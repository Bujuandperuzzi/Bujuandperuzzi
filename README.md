import React, { useState } from 'react';
import axios from 'axios';

const PlaceBet = () => {
  const [matchId, setMatchId] = useState('');
  const [amount, setAmount] = useState('');
  const [betType, setBetType] = useState('win');
  const [message, setMessage] = useState('');

  const handleSubmit = async (event) => {
    event.preventDefault();
    try {
      const response = await axios.post('/api/place-bet', {
        matchId,
        amount,
        betType
      });
      setMessage(response.data.message);
    } catch (error) {
      setMessage('Error placing bet.');
    }
  };

  return (
    <div>
      <h2>Place Your Bet</h2>
      <form onSubmit={handleSubmit}>
        <div>
          <label>Match ID:</label>
          <input
            type="text"
            value={matchId}
            onChange={(e) => setMatchId(e.target.value)}
            required
          />
        </div>
        <div>
          <label>Amount:</label>
          <input
            type="number"
            value={amount}
            onChange={(e) => setAmount(e.target.value)}
            required
          />
        </div>
        <div>
          <label>Bet Type:</label>
          <select value={betType} onChange={(e) => setBetType(e.target.value)}>
            <option value="win">Win</option>
            <option value="draw">Draw</option>
            <option value="lose">Lose</option>
          </select>
        </div>
        <button type="submit">Place Bet</button>
      </form>
      {message && <p>{message}</p>}
    </div>
  );
};

export default PlaceBet;
