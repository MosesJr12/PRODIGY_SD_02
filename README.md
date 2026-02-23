import random
import time

# ==============================
# BIBLE QUESTION DATABASE
# ==============================

questions = {
    "Easy": [
        {
            "question": "Who built the ark?",
            "options": ["A. Moses", "B. Noah", "C. Abraham", "D. David"],
            "answer": "B"
        },
        {
            "question": "Where was Jesus born?",
            "options": ["A. Nazareth", "B. Bethlehem", "C. Jerusalem", "D. Rome"],
            "answer": "B"
        },
        {
            "question": "Who betrayed Jesus?",
            "options": ["A. Peter", "B. John", "C. Judas Iscariot", "D. Matthew"],
            "answer": "C"
        },
        {
            "question": "Who killed Goliath?",
            "options": ["A. Saul", "B. David", "C. Samuel", "D. Jonathan"],
            "answer": "B"
        }
    ],

    "Medium": [
        {
            "question": "How many plagues were sent on Egypt?",
            "options": ["A. 7", "B. 10", "C. 12", "D. 40"],
            "answer": "B"
        },
        {
            "question": "Who was swallowed by a great fish?",
            "options": ["A. Elijah", "B. Jonah", "C. Isaiah", "D. Ezekiel"],
            "answer": "B"
        },
        {
            "question": "Which king built the first Temple in Jerusalem?",
            "options": ["A. David", "B. Solomon", "C. Hezekiah", "D. Josiah"],
            "answer": "B"
        },
        {
            "question": "Who denied Jesus three times?",
            "options": ["A. Thomas", "B. Peter", "C. James", "D. Andrew"],
            "answer": "B"
        },
        {
            "question": "What is the shortest verse in the Bible?",
            "options": [
                "A. Rejoice always",
                "B. Jesus wept",
                "C. Pray continually",
                "D. God is love"
            ],
            "answer": "B"
        }
    ],

    "Hard": [
        {
            "question": "Who was the mother of the prophet Samuel?",
            "options": ["A. Ruth", "B. Hannah", "C. Elizabeth", "D. Miriam"],
            "answer": "B"
        },
        {
            "question": "Which book comes immediately after Acts?",
            "options": ["A. Romans", "B. 1 Corinthians", "C. Hebrews", "D. Galatians"],
            "answer": "A"
        },
        {
            "question": "How many books are in the Old Testament (Protestant canon)?",
            "options": ["A. 27", "B. 39", "C. 46", "D. 66"],
            "answer": "B"
        },
        {
            "question": "Who interpreted Pharaoh's dreams?",
            "options": ["A. Daniel", "B. Joseph", "C. Moses", "D. Aaron"],
            "answer": "B"
        },
        {
            "question": "Which prophet confronted King David about Bathsheba?",
            "options": ["A. Samuel", "B. Elijah", "C. Nathan", "D. Isaiah"],
            "answer": "C"
        },
        {
            "question": "What was Paul's Hebrew name?",
            "options": ["A. Simeon", "B. Saul", "C. Silas", "D. Barnabas"],
            "answer": "B"
        },
        {
            "question": "In Revelation, how many churches were addressed?",
            "options": ["A. 5", "B. 7", "C. 10", "D. 12"],
            "answer": "B"
        }
    ]
}

# ==============================
# GAME FUNCTIONS
# ==============================

def slow_print(text):
    for char in text:
        print(char, end="", flush=True)
        time.sleep(0.02)
    print()

def choose_difficulty():
    print("\nSelect Difficulty Level:")
    levels = list(questions.keys())
    for i, level in enumerate(levels, 1):
        print(f"{i}. {level}")
    
    while True:
        try:
            choice = int(input("Enter choice: "))
            if 1 <= choice <= len(levels):
                return levels[choice - 1]
            else:
                print("Invalid choice.")
        except:
            print("Enter a valid number.")

def ask_question(q):
    print("\n" + q["question"])
    for option in q["options"]:
        print(option)
    
    while True:
        answer = input("Your answer (A/B/C/D): ").upper()
        if answer in ["A", "B", "C", "D"]:
            break
        else:
            print("Please enter A, B, C, or D.")
    
    if answer == q["answer"]:
        print("✅ Correct!")
        return True
    else:
        print(f"❌ Wrong! Correct answer was {q['answer']}.")
        return False

def play_game():
    score = 0
    slow_print("📖 Welcome to the Advanced Bible Guessing Game!")
    
    difficulty = choose_difficulty()
    selected_questions = questions[difficulty]
    random.shuffle(selected_questions)
    
    for q in selected_questions:
        if ask_question(q):
            score += 1
    
    total = len(selected_questions)
    percentage = (score / total) * 100
    
    print("\n======================")
    print("📊 FINAL RESULTS")
    print("======================")
    print(f"Difficulty: {difficulty}")
    print(f"Score: {score}/{total}")
    print(f"Percentage: {percentage:.1f}%")
    
    if percentage == 100:
        print("🏆 Bible Scholar Level!")
    elif percentage >= 75:
        print("👏 Strong knowledge!")
    elif percentage >= 50:
        print("👍 Good effort!")
    else:
        print("📖 Time for deeper study!")

def main():
    while True:
        play_game()
        replay = input("\nPlay again? (yes/no): ").lower()
        if replay != "yes":
            print("🙏 Thanks for playing! Stay blessed!")
            break

if __name__ == "__main__":
    main()
