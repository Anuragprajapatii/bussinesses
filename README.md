<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Wedding WhatsApp Message Generator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      max-width: 600px;
      margin: auto;
      background-color: #f7f7f7;
    }

    h2 {
      text-align: center;
    }

    input, button, textarea {
      width: 100%;
      margin-top: 10px;
      padding: 10px;
      font-size: 16px;
      
    }

    textarea {
      height: 400px;
      resize: vertical;
    }

    .button-group {
      display: flex;
      gap: 10px;
      margin-top: 10px;
    }
    .whatsappbtn{
      background-color: rgb(47, 204, 47);
      border: none;
      border-radius: 20px;
    }
    .messagebtn{
      background-color: rgba(255, 94, 94, 0.722);
      border: none;
      border-radius: 20px;
    }

    @media (max-width: 480px) {
      input, button, textarea {
        font-size: 15px;
      }
      .button-group {
        flex-direction: column;
      }
    }
  </style>
</head>
<body>

<h2>WhatsApp Message Generator</h2>

<label for="guests">Enter Number of Guests:</label>
<input type="number" id="guests" value="130" placeholder="e.g., 130" />

<div class="button-group">
  <button onclick="generateMessage()" class="messagebtn">Generate Message</button>
  <button onclick="shareViaWhatsApp()" class="whatsappbtn">Share via WhatsApp</button>
</div>

<textarea id="output" readonly></textarea>

<script>
let generatedMessage = '';

function generateMessage() {
  const guests = parseInt(document.getElementById('guests').value);

  if (isNaN(guests) || guests <= 0) {
    alert("Please enter a valid number of guests.");
    return;
  }

  const roomRate = 4500;
  const nights = 2;
  const lunchRate = 500;
  const hiTeaRate = 300;
  const dinnerRate = 500;
  const galaDinnerRate = 2000;
  const breakfastRate = 350;
  const djDecoration = 340000;
  const djLicense = 10000;

  let rooms = 40;
  let roomDetails = "40 rooms";

  if (guests <= 80) {
    rooms = 22;
    roomDetails = "22 rooms (16 dual/triple sharing + 6 quad sharing)";
  }

  const accommodation = roomRate * rooms * nights;
  const day1Lunch = lunchRate * guests;
  const day1HiTea = hiTeaRate * guests;
  const day1Dinner = dinnerRate * guests;
  const day1Total = day1Lunch + day1HiTea + day1Dinner;

  const day2Breakfast = breakfastRate * guests;
  const day2Lunch = lunchRate * guests;
  const day2Gala = galaDinnerRate * guests;
  const day2Total = day2Breakfast + day2Lunch + day2Gala;

  const day3Breakfast = breakfastRate * guests;
  const day3Total = day3Breakfast;

  const foodTotal = day1Total + day2Total + day3Total;
  const grandTotal = accommodation + foodTotal + djDecoration;

  generatedMessage = `🛏️ Accommodation
${roomDetails} × ₹${roomRate} × ${nights} nights = ₹${accommodation.toLocaleString()}

📅 Day 1 (Check-In):

Welcome Drink (Included)

Lunch: ₹${lunchRate} × ${guests} = ₹${day1Lunch.toLocaleString()}
Hi-Tea: ₹${hiTeaRate} × ${guests} = ₹${day1HiTea.toLocaleString()}
Dinner: ₹${dinnerRate} × ${guests} = ₹${day1Dinner.toLocaleString()}

Total Day 1: ₹${day1Total.toLocaleString()}

📅 Day 2 (Stay Over):

Breakfast: ₹${breakfastRate} × ${guests} = ₹${day2Breakfast.toLocaleString()}
Lunch: ₹${lunchRate} × ${guests} = ₹${day2Lunch.toLocaleString()}
Gala Dinner: ₹${galaDinnerRate} × ${guests} = ₹${day2Gala.toLocaleString()}

Total Day 2: ₹${day2Total.toLocaleString()}

📅 Day 3 (Check-Out):

Breakfast: ₹${breakfastRate} × ${guests} = ₹${day3Breakfast.toLocaleString()}

Total Day 3: ₹${day3Total.toLocaleString()}

🎧 DJ + Decoration (2 Days): ₹${djDecoration.toLocaleString()}

💰 Grand Total =
Accommodation: ₹${accommodation.toLocaleString()}
Food (Day 1+2+3): ₹${foodTotal.toLocaleString()}
DJ & Decoration: ₹${djDecoration.toLocaleString()}
= ₹${grandTotal.toLocaleString()}

Note: An additional ₹${djLicense.toLocaleString()} DJ license fee is paid to the camp union to maintain forest and wildlife decorum. This is only allowed for special occasions like weddings.

📞 Contact us: +91 9084340720  
🌐 Website: www.himriverrishikesh.com`;

  document.getElementById('output').value = generatedMessage;
}

function shareViaWhatsApp() {
  if (!generatedMessage) {
    alert("Please generate the message first.");
    return;
  }
  const encodedMessage = encodeURIComponent(generatedMessage);
  const whatsappUrl = `https://wa.me/?text=${encodedMessage}`;
  window.open(whatsappUrl, '_blank');
}
</script>

</body>
</html>
