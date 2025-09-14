#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>
#include <time.h>

// function to convert string to lowercase (for case-insensitive comparison)
void toLowerCase(char str[]) {
    for (int i = 0; str[i]; i++) {
        str[i] = tolower(str[i]);
    }
}

struct Question {
    char state[50];
    char capital[50];
    char options[4][50];
};

// function to shuffle questions randomly
void shuffle(struct Question quiz[], int n) {
    for (int i = n - 1; i > 0; i--) {
        int j = rand() % (i + 1);
        struct Question temp = quiz[i];
        quiz[i] = quiz[j];
        quiz[j] = temp;
    }
}

int main() {
    struct Question quiz[] = {
        {"Andhra Pradesh", "Amaravati", {"Amaravati", "Hyderabad", "Vijayawada", "Visakhapatnam"}},
        {"Arunachal Pradesh", "Itanagar", {"Aizawl", "Kohima", "Itanagar", "Gangtok"}},
        {"Assam", "Dispur", {"Dispur", "Guwahati", "Shillong", "Imphal"}},
        {"Bihar", "Patna", {"Patna", "Ranchi", "Gaya", "Muzaffarpur"}},
        {"Chhattisgarh", "Raipur", {"Raipur", "Bilaspur", "Durg", "Korba"}},
        {"Goa", "Panaji", {"Panaji", "Vasco", "Margao", "Mapusa"}},
        {"Gujarat", "Gandhinagar", {"Gandhinagar", "Ahmedabad", "Surat", "Rajkot"}},
        {"Haryana", "Chandigarh", {"Chandigarh", "Faridabad", "Ambala", "Panipat"}},
        {"Himachal Pradesh", "Shimla", {"Shimla", "Mandi", "Kullu", "Manali"}},
        {"Jharkhand", "Ranchi", {"Ranchi", "Jamshedpur", "Dhanbad", "Bokaro"}},
        {"Karnataka", "Bengaluru", {"Mysuru", "Bengaluru", "Mangalore", "Hubli"}},
        {"Kerala", "Thiruvananthapuram", {"Kochi", "Kozhikode", "Thiruvananthapuram", "Thrissur"}},
        {"Madhya Pradesh", "Bhopal", {"Indore", "Gwalior", "Bhopal", "Jabalpur"}},
        {"Maharashtra", "Mumbai", {"Pune", "Nagpur", "Mumbai", "Nashik"}},
        {"Manipur", "Imphal", {"Agartala", "Imphal", "Aizawl", "Kohima"}},
        {"Meghalaya", "Shillong", {"Shillong", "Aizawl", "Gangtok", "Dispur"}},
        {"Mizoram", "Aizawl", {"Kohima", "Imphal", "Aizawl", "Shillong"}},
        {"Nagaland", "Kohima", {"Kohima", "Dimapur", "Shillong", "Itanagar"}},
        {"Odisha", "Bhubaneswar", {"Cuttack", "Bhubaneswar", "Rourkela", "Puri"}},
        {"Punjab", "Chandigarh", {"Amritsar", "Ludhiana", "Chandigarh", "Jalandhar"}},
        {"Rajasthan", "Jaipur", {"Jodhpur", "Udaipur", "Jaipur", "Ajmer"}},
        {"Sikkim", "Gangtok", {"Gangtok", "Shillong", "Kohima", "Aizawl"}},
        {"Tamil Nadu", "Chennai", {"Madurai", "Chennai", "Coimbatore", "Tiruchirappalli"}},
        {"Telangana", "Hyderabad", {"Hyderabad", "Warangal", "Karimnagar", "Nizamabad"}},
        {"Tripura", "Agartala", {"Agartala", "Imphal", "Shillong", "Aizawl"}},
        {"Uttar Pradesh", "Lucknow", {"Kanpur", "Varanasi", "Lucknow", "Agra"}},
        {"Uttarakhand", "Dehradun", {"Dehradun", "Haridwar", "Nainital", "Rishikesh"}},
        {"West Bengal", "Kolkata", {"Howrah", "Durgapur", "Siliguri", "Kolkata"}}
    };

    int totalQuestions = sizeof(quiz) / sizeof(quiz[0]);
    int score = 0, correct = 0, wrong = 0;
    char answer[50], correctCapital[50], userAnswer[50];

    srand(time(NULL)); // seed random generator
    shuffle(quiz, totalQuestions); // shuffle questions

    printf("\n*** Indian States and Capitals Quiz ***\n\n");

    for (int i = 0; i < totalQuestions; i++) {
        printf("Q%d: What is the capital of %s?\n", i + 1, quiz[i].state);

        // show options (for hint)
        printf("Options: ");
        for (int j = 0; j < 4; j++) {
            printf("%s", quiz[i].options[j]);
            if (j < 3) printf(", ");
        }

        printf("\nYour Answer: ");
        scanf(" %[^\n]", answer);  // read full line input

        // convert both user input and correct answer to lowercase
        strcpy(userAnswer, answer);
        strcpy(correctCapital, quiz[i].capital);
        toLowerCase(userAnswer);
        toLowerCase(correctCapital);

        if (strcmp(userAnswer, correctCapital) == 0) {
            printf("✅ Correct!\n\n");
            score++;
            correct++;
        } else {
            printf("❌ Wrong! Correct Answer: %s\n\n", quiz[i].capital);
            wrong++;
        }
    }

    printf("\n*** Quiz Completed! ***\n");
    printf("Total Questions: %d\n", totalQuestions);
    printf("Correct Answers: %d\n", correct);
    printf("Wrong Answers: %d\n", wrong);
    printf("Your Score: %d / %d\n", score, totalQuestions);

    return 0;
}
