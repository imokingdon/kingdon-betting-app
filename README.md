# kingdon-betting-app
// Kingdon Cricket Betting App // Frontend: React.js

import React, { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button";

const matches = [ { id: 1, teamA: "বাংলাদেশ", teamB: "ভারত", time: "আজ রাত ৮টা" }, { id: 2, teamA: "অস্ট্রেলিয়া", teamB: "ইংল্যান্ড", time: "আগামীকাল সকাল ১০টা" }, ];

export default function Home() { const [user, setUser] = useState(null); const [username, setUsername] = useState(""); const [balance, setBalance] = useState(1000); const [bet, setBet] = useState(0);

const handleLogin = () => { if (username.trim() !== "") { setUser({ name: username }); alert("লগইন সফল হয়েছে"); } else { alert("নাম দিন"); } };

const placeBet = (amount) => { if (!user) return alert("আগে লগইন করুন"); if (amount > 0 && amount <= balance) { setBalance(balance - amount); alert("বাজি ধরা হয়েছে!"); } else { alert("সঠিক পরিমাণ দিন।"); } };

return ( <div className="p-4 space-y-4"> <h1 className="text-2xl font-bold text-green-600">Kingdon – ক্রিকেট বাজি</h1>

{!user ? (
    <div className="space-y-2">
      <input
        type="text"
        placeholder="আপনার নাম"
        className="border p-2 rounded"
        onChange={(e) => setUsername(e.target.value)}
      />
      <br />
      <Button onClick={handleLogin}>লগইন করুন</Button>
    </div>
  ) : (
    <div>
      <p>স্বাগতম, {user.name}!</p>
      <p>আপনার ব্যালেন্স: {balance} টাকা</p>

      {matches.map((match) => (
        <Card key={match.id} className="bg-white shadow rounded-xl p-4 my-4">
          <CardContent>
            <p className="font-semibold">
              {match.teamA} বনাম {match.teamB}
            </p>
            <p>সময়: {match.time}</p>
            <input
              type="number"
              placeholder="বাজির পরিমাণ"
              className="border rounded p-1 mt-2 mr-2"
              onChange={(e) => setBet(Number(e.target.value))}
            />
            <Button onClick={() => placeBet(bet)}>বাজি দিন</Button>
          </CardContent>
        </Card>
      ))}
    </div>
  )}
</div>

); }

