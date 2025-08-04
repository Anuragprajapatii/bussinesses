<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Wedding WhatsApp Message Generator</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div class="bg-white p-8 rounded-xl shadow-lg w-full max-w-2xl">
        <h2 class="text-3xl font-bold text-center mb-6 text-gray-800">Him River Resort Wedding Query Message</h2>

        <!-- Room Rate Input -->
        <div class="mb-4">
            <label for="roomRate" class="block text-sm font-medium text-gray-700">Room Price per Night (₹)</label>
            <input type="number" id="roomRate" value="4500" placeholder="e.g., 4500"
                   class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
        </div>

        <!-- Day 1 Inputs -->
        <div class="bg-gray-50 p-4 rounded-md mb-4">
            <h3 class="text-lg font-semibold mb-2 text-gray-700">Day 1 (Check-In)</h3>
            <div class="flex flex-col sm:flex-row sm:space-x-4 space-y-4 sm:space-y-0">
                <div class="w-full sm:w-1/2">
                    <label for="guestsDay1" class="block text-sm font-medium text-gray-700">Number of Guests</label>
                    <input type="number" id="guestsDay1"  placeholder="number of person"
                           class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
                </div>
                <div class="w-full sm:w-1/2">
                    <label for="roomsDay1" class="block text-sm font-medium text-gray-700">Number of Rooms</label>
                    <input type="number" id="roomsDay1"  placeholder="number of romms"
                           class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
                </div>
            </div>
        </div>

        <!-- Day 2 Inputs -->
        <div class="bg-gray-50 p-4 rounded-md mb-4">
            <h3 class="text-lg font-semibold mb-2 text-gray-700">Day 2 (Stay Over)</h3>
            <div class="flex flex-col sm:flex-row sm:space-x-4 space-y-4 sm:space-y-0">
                <div class="w-full sm:w-1/2">
                    <label for="guestsDay2" class="block text-sm font-medium text-gray-700">Number of Guests</label>
                    <input type="number" id="guestsDay2" placeholder="Number of guests"
                           class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
                </div>
                <div class="w-full sm:w-1/2">
                    <label for="roomsDay2" class="block text-sm font-medium text-gray-700">Number of Rooms</label>
                    <input type="number" id="roomsDay2"  placeholder="Number of rooms"
                           class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
                </div>
            </div>
        </div>

        <!-- Day 3 Inputs -->
        <div class="bg-gray-50 p-4 rounded-md mb-4">
            <h3 class="text-lg font-semibold mb-2 text-gray-700">Day 3 (Check-Out)</h3>
            <div class="w-full">
                <label for="guestsDay3" class="block text-sm font-medium text-gray-700">Number of Guests</label>
                <input type="number" id="guestsDay3"  placeholder="Number of person"
                       class="mt-1 block w-full p-3 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 transition-colors">
            </div>
        </div>

        <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4 mb-4">
            <button onclick="generateMessage()"
                    class="w-full flex-1 bg-green-600 text-white font-bold py-3 px-4 rounded-md shadow-md hover:bg-green-700 transition-colors">
                Generate Message
            </button>
            <button onclick="copyToClipboard()"
                    class="w-full flex-1 bg-indigo-600 text-white font-bold py-3 px-4 rounded-md shadow-md hover:bg-indigo-700 transition-colors">
                Copy to Clipboard
            </button>
        </div>
        <button onclick="sendViaWhatsApp()"
                class="w-full bg-teal-600 text-white font-bold py-3 px-4 rounded-md shadow-md hover:bg-teal-700 transition-colors">
            Send via WhatsApp
        </button>

        <textarea id="output" readonly
                  class="mt-4 block w-full p-4 border border-gray-300 rounded-md shadow-sm bg-gray-50 text-gray-800 focus:ring-indigo-500 focus:border-indigo-500 h-96 resize-y"></textarea>
    </div>

    <!-- Custom Alert Message Box -->
    <div id="messageBox" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden items-center justify-center transition-opacity duration-300">
        <div class="bg-white p-6 rounded-lg shadow-xl text-center max-w-sm w-full">
            <p id="messageText" class="text-gray-800 mb-4"></p>
            <button onclick="hideMessageBox()" class="px-6 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700 transition-colors">OK</button>
        </div>
    </div>

    <script>
        // Global variables for the message box
        const messageBox = document.getElementById('messageBox');
        const messageText = document.getElementById('messageText');

        // Function to show the custom message box
        function showMessageBox(message) {
            messageText.textContent = message;
            messageBox.style.display = 'flex';
        }

        // Function to hide the custom message box
        function hideMessageBox() {
            messageBox.style.display = 'none';
        }

        function generateMessage() {
            const roomRate = parseInt(document.getElementById('roomRate').value);
            const guestsDay1 = parseInt(document.getElementById('guestsDay1').value);
            const roomsDay1 = parseInt(document.getElementById('roomsDay1').value);
            const guestsDay2 = parseInt(document.getElementById('guestsDay2').value);
            const roomsDay2 = parseInt(document.getElementById('roomsDay2').value);
            const guestsDay3 = parseInt(document.getElementById('guestsDay3').value);

            // Validate inputs
            if (isNaN(roomRate) || isNaN(guestsDay1) || isNaN(roomsDay1) || isNaN(guestsDay2) || isNaN(roomsDay2) || isNaN(guestsDay3) || roomRate <= 0 || guestsDay1 <= 0 || guestsDay2 <= 0 || guestsDay3 <= 0 || roomsDay1 <= 0 || roomsDay2 <= 0) {
                showMessageBox("Please enter a valid number for all fields.");
                return;
            }

            // Fixed rates
            const lunchRate = 500;
            const hiTeaRate = 300;
            const dinnerRate = 500;
            const galaDinnerRate = 2000;
            const breakfastRate = 350;
            const djDecoration = 340000;
            const djLicense = 10000;

            // Day 1 Calculations
            const day1Accommodation = roomRate * roomsDay1;
            const day1Lunch = lunchRate * guestsDay1;
            const day1HiTea = hiTeaRate * guestsDay1;
            const day1Dinner = dinnerRate * guestsDay1;
            const day1Total = day1Accommodation + day1Lunch + day1HiTea + day1Dinner;

            // Day 2 Calculations
            const day2Accommodation = roomRate * roomsDay2;
            const day2Breakfast = breakfastRate * guestsDay2;
            const day2Lunch = lunchRate * guestsDay2;
            const day2Gala = galaDinnerRate * guestsDay2;
            const day2Total = day2Accommodation + day2Breakfast + day2Lunch + day2Gala;

            // Day 3 Calculations
            const day3Breakfast = breakfastRate * guestsDay3;
            const day3Total = day3Breakfast;

            // Grand Totals
            const accommodationTotal = day1Accommodation + day2Accommodation;
            const foodTotal = (day1Lunch + day1HiTea + day1Dinner) + (day2Breakfast + day2Lunch + day2Gala) + day3Breakfast;
            const grandTotal = accommodationTotal + foodTotal + djDecoration + djLicense;

            // Format the message
            const message = `📅 Day 1 (Check-In):
🛏️ Accommodation: ${roomsDay1} rooms × ₹${roomRate.toLocaleString()} = ₹${day1Accommodation.toLocaleString()}
Welcome Drink (Included)
Lunch: ₹${lunchRate.toLocaleString()} × ${guestsDay1} guests = ₹${day1Lunch.toLocaleString()}
Hi-Tea: ₹${hiTeaRate.toLocaleString()} × ${guestsDay1} guests = ₹${day1HiTea.toLocaleString()}
Dinner: ₹${dinnerRate.toLocaleString()} × ${guestsDay1} guests = ₹${day1Dinner.toLocaleString()}
Total Day 1: ₹${day1Total.toLocaleString()}

📅 Day 2 (Stay Over):
🛏️ Accommodation: ${roomsDay2} rooms × ₹${roomRate.toLocaleString()} = ₹${day2Accommodation.toLocaleString()}
Breakfast: ₹${breakfastRate.toLocaleString()} × ${guestsDay2} guests = ₹${day2Breakfast.toLocaleString()}
Lunch: ₹${lunchRate.toLocaleString()} × ${guestsDay2} guests = ₹${day2Lunch.toLocaleString()}
Gala Dinner: ₹${galaDinnerRate.toLocaleString()} × ${guestsDay2} guests = ₹${day2Gala.toLocaleString()}
Total Day 2: ₹${day2Total.toLocaleString()}

📅 Day 3 (Check-Out):
Breakfast: ₹${breakfastRate.toLocaleString()} × ${guestsDay3} guests = ₹${day3Breakfast.toLocaleString()}
Total Day 3: ₹${day3Total.toLocaleString()}

🎧 DJ + Decoration (2 Days): ₹${djDecoration.toLocaleString()}

💰 Grand Total
Accommodation: ₹${accommodationTotal.toLocaleString()}
Food (Day 1+2+3): ₹${foodTotal.toLocaleString()}
DJ & Decoration: ₹${djDecoration.toLocaleString()}
DJ License Fee: ₹${djLicense.toLocaleString()}
= ₹${grandTotal.toLocaleString()}

Note: An additional ₹${djLicense.toLocaleString()} DJ license fee is paid to the camp union to maintain forest and wildlife decorum. This is only allowed for special occasions like weddings.

📞 Contact us: +91 9084340720  / +91 9758114823
🌐 Website: www.himriverrishikesh.com
📘 Facebook: https://www.facebook.com/himriverresortss?mibextid=ZbWKwL
📸 Instagram: https://www.instagram.com/himriver.resort/
🗺️ Google Page: https://maps.app.goo.gl/CETcKnDmL1Brq7KK7`;

            document.getElementById('output').value = message;
        }

        function copyToClipboard() {
            const output = document.getElementById('output');
            if (output.value) {
                output.select();
                output.setSelectionRange(0, 99999); // For mobile
                document.execCommand("copy");
                showMessageBox("Message copied to clipboard!");
            } else {
                showMessageBox("Please generate a message first.");
            }
        }

        function sendViaWhatsApp() {
            const output = document.getElementById('output');
            const message = output.value;

            if (message) {
                const encodedMessage = encodeURIComponent(message);
                const whatsappUrl = `whatsapp://send?text=${encodedMessage}`;
                window.location.href = whatsappUrl;
            } else {
                showMessageBox("Please generate a message first.");
            }
        }
    </script>
</body>
</html>
