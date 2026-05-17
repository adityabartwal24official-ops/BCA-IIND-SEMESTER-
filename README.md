# BCA-IIND-SEMESTER-


#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

// -------- DESIGN FUNCTION --------
void line() {
    cout << "\n========================================\n";
}

void title() {
    line();
    cout << "   SMART ACADEMIC PLANNER SYSTEM\n";
    line();
}

// -------- STUDY TASK CLASS --------
class StudyTask {
public:
    string subject;
    int hours;

    void addTask() {
        ofstream file("study.txt", ios::app);

        line();
        cout << "        ADD STUDY TASK\n";
        line();

        cout << "Enter Subject: ";
        cin >> subject;
        cout << "Enter Study Hours: ";
        cin >> hours;

        file << subject << " " << hours << endl;
        file.close();

        cout << "\n✔ Task Added Successfully!\n";
    }

    void viewTasks() {
        ifstream file("study.txt");

        line();
        cout << "        STUDY PLAN\n";
        line();

        cout << left << setw(15) << "Subject" << setw(10) << "Hours\n";
        line();

        while (file >> subject >> hours) {
            cout << left << setw(15) << subject << setw(10) << hours << endl;
        }

        file.close();
    }
};

// -------- PERFORMANCE CLASS --------
class Performance {
public:
    int marks[5];
    float percentage;

    void enterMarks() {
        ofstream file("marks.txt");

        line();
        cout << "     ENTER SUBJECT MARKS\n";
        line();

        for (int i = 0; i < 5; i++) {
            cout << "Subject " << i + 1 << ": ";
            cin >> marks[i];
            file << marks[i] << " ";
        }

        file.close();
        cout << "\n✔ Marks Saved Successfully!\n";
    }

    void analyze() {
        ifstream file("marks.txt");

        int sum = 0;

        line();
        cout << "     PERFORMANCE ANALYSIS\n";
        line();

        for (int i = 0; i < 5; i++) {
            file >> marks[i];
            sum += marks[i];
        }

        percentage = sum / 5.0;

        cout << "\nPercentage: " << percentage << "%\n";

        // Grade
        if (percentage >= 90)
            cout << "Grade: A\n";
        else if (percentage >= 75)
            cout << "Grade: B\n";
        else if (percentage >= 60)
            cout << "Grade: C\n";
        else
            cout << "Grade: Need Improvement\n";

        // Weak Subject
        int min = marks[0], index = 0;
        for (int i = 1; i < 5; i++) {
            if (marks[i] < min) {
                min = marks[i];
                index = i;
            }
        }

        cout << "Weak Subject: Subject " << index + 1 << endl;

        file.close();
    }
};

// -------- MAIN FUNCTION --------
int main() {
    StudyTask task;
    Performance perf;

    int choice;

    do {
        title();

        cout << "1. Add Study Task\n";
        cout << "2. View Study Plan\n";
        cout << "3. Enter Marks\n";
        cout << "4. Analyze Performance\n";
        cout << "5. Exit\n";

        line();
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            task.addTask();
            break;

        case 2:
            task.viewTasks();
            break;

        case 3:
            perf.enterMarks();
            break;

        case 4:
            perf.analyze();
            break;

        case 5:
            cout << "\nThank You for Using the System!\n";
            break;

        default:
            cout << "\nInvalid Choice!\n";
        }

    } while (choice != 5);

    return 0;
}