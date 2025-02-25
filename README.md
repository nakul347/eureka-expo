import React, { useState, useEffect } from "react";
import { initializeApp } from "firebase/app";
import { getFirestore, collection, addDoc, getDocs } from "firebase/firestore";
import "./styles.css";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

export default function App() {
  const [name, setName] = useState("");
  const [feedback, setFeedback] = useState("");
  const [feedbacks, setFeedbacks] = useState([]);
  const [showFeedback, setShowFeedback] = useState(false);

  useEffect(() => {
    fetchFeedbacks();
  }, []);

  const submitFeedback = async () => {
    if (name && feedback) {
      await addDoc(collection(db, "feedbacks"), { name, feedback });
      alert("Thank you for your review!");
      setName("");
      setFeedback("");
      fetchFeedbacks();
    }
  };

  const fetchFeedbacks = async () => {
    const querySnapshot = await getDocs(collection(db, "feedbacks"));
    setFeedbacks(querySnapshot.docs.map(doc => doc.data()));
  };

  return (
    <div className="app">
      <header>
        <img src="https://media-exp1.licdn.com/dms/image/C4D0BAQHxSgco_-fddg/company-logo_200_200/0?e=2159024400&v=beta&t=-Kore7RpBT8kDcUM2UDlyh4IXyrBqHvVR-seDRuTPVI" alt="Chaitanya Logo" className="chaitanya-logo" />
        <h1 className="eureka">EUREKA</h1>
        <h2>Science Expo</h2>
        <h3>Feedback Website</h3>
      </header>

      <div className="feedback-form">
        <input type="text" placeholder="Enter your name" value={name} onChange={(e) => setName(e.target.value)} />
        <textarea placeholder="Enter your feedback" value={feedback} onChange={(e) => setFeedback(e.target.value)}></textarea>
        <button onClick={submitFeedback}>Done</button>
      </div>

      {name === "8888" && !showFeedback && (
        <button onClick={() => setShowFeedback(true)}>View Feedback</button>
      )}

      {showFeedback && (
        <div className="feedback-list">
          <h2>All Feedback</h2>
          {feedbacks.map((f, index) => (
            <p key={index}><strong>{f.name}:</strong> {f.feedback}</p>
          ))}
          <button onClick={() => setShowFeedback(false)}>Hide</button>
        </div>
      )}
    </div>
  );
}
