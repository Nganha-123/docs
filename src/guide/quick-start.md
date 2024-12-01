const quizData = [
  {
    question: "What kind of ambiance do you prefer for your dinner?",
    options: {
      A: "Warm, culturally immersive with a touch of tradition",
      B: "High-energy, with entertaining service features",
      C: "Luxurious, quiet, and refined",
      D: "Casual and modern, perfect for takeaway or quick dine-in"
    }
  },
  {
    question: "What’s your ideal budget per person?",
    options: {
      A: "400,000–500,000 VNĐ",
      B: "500,000–700,000 VNĐ",
      C: "450,000–600,000 VNĐ",
      D: "350,000–450,000 VNĐ"
    }
  },
  {
    question: "Are you looking for more personalized service or self-service?",
    options: {
      A: "A traditional hotpot served in an elegant, family-style manner",
      B: "Full-on personalized service with extras like free manicures",
      C: "High-quality service but with a focus on a gourmet experience",
      D: "Quick, efficient, and even takeaway-ready"
    }
  },
  {
    question: "Who are you dining with tonight?",
    options: {
      A: "Close family or friends who love authentic Taiwanese flavors",
      B: "Colleagues or a large group looking for fun and pampering",
      C: "A date or special occasion that calls for sophistication",
      D: "Friends looking for a quick, budget-friendly option"
    }
  },
  {
    question: "What’s most important to you about the food?",
    options: {
      A: "Unique, authentic broths with herbal Taiwanese flavors",
      B: "A wide variety of fresh ingredients and playful dipping sauces",
      C: "Premium cuts of meat and gourmet-style presentation",
      D: "Accessibility, simplicity, and tasty options for takeout"
    }
  },
  {
    question: "What’s the deciding factor for your choice tonight?",
    options: {
      A: "Traditional vibes and unique tastes",
      B: "Memorable service and exciting interactions",
      C: "Sophisticated dining and attention to detail",
      D: "Convenient, affordable, and modern dining"
    }
  }
];

const resultMapping = {
  A: "Manwah",
  B: "Haidilao",
  C: "Hutong",
  D: "Chao Xian"
};

let scores = { A: 0, B: 0, C: 0, D: 0 };
let currentQuestion = 0;

function loadQuestion() {
  const quizDiv = document.getElementById("quiz");
  quizDiv.innerHTML = "";

  if (currentQuestion < quizData.length) {
    const questionData = quizData[currentQuestion];
    const questionDiv = document.createElement("div");
    questionDiv.className = "question";
    questionDiv.innerHTML = `<h3>${questionData.question}</h3>`;

    const optionsDiv = document.createElement("div");
    optionsDiv.className = "options";

    for (const [key, value] of Object.entries(questionData.options)) {
      const button = document.createElement("button");
      button.innerText = value;
      button.onclick = () => {
        scores[key]++;
        currentQuestion++;
        loadQuestion();
      };
      optionsDiv.appendChild(button);
    }

    questionDiv.appendChild(optionsDiv);
    quizDiv.appendChild(questionDiv);
  } else {
    showResult();
  }
}

function showResult() {
  const quizDiv = document.getElementById("quiz");
  quizDiv.style.display = "none";

  const resultDiv = document.getElementById("result");
  const topScore = Object.keys(scores).reduce((a, b) =>
    scores[a] > scores[b] ? a : b
  );

  document.getElementById("brand").innerText = resultMapping[topScore];
  resultDiv.style.display = "block";
}

// Start the quiz
loadQuestion();
