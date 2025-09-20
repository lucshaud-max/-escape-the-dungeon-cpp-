// dungeon_adventure.cpp
// Escape the Dungeon – A Text-Based Adventure
// Build: g++ -std=c++17 -Wall -Wextra -O2 dungeon_adventure.cpp -o dungeon
// Run:   ./dungeon

#include <iostream>
#include <limits>
#include <string>
using namespace std;

// Helper for safe numeric input
int getChoice(int min, int max) {
    int choice;
    while (true) {
        cout << "> ";
        if (cin >> choice && choice >= min && choice <= max) {
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            return choice;
        }
        cout << "Invalid input. Please enter a number between " 
             << min << " and " << max << ".\n";
        cin.clear();
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
    }
}

// Helper for yes/no input
bool getYesNo(string prompt) {
    while (true) {
        cout << prompt << " (y/n)\n> ";
        string s;
        getline(cin, s);
        if (!s.empty()) {
            char c = tolower(s[0]);
            if (c == 'y') return true;
            if (c == 'n') return false;
        }
        cout << "Please type y or n.\n";
    }
}

int main() {
    cout << "============================\n";
    cout << "  Escape the Dungeon Game\n";
    cout << "============================\n\n";
    cout << "You wake up in a cold, dark dungeon. "
         << "Your goal is to find a way out...\n\n";

    // --- First decision: nested if/else ---
    cout << "You see two paths:\n";
    cout << "  1) A narrow tunnel with dripping water.\n";
    cout << "  2) A stairway leading upward.\n";
    int firstChoice = getChoice(1, 2);

    if (firstChoice == 1) {
        cout << "\nYou crawl into the tunnel. It's tight and dark...\n";
        if (getYesNo("Do you want to light a torch?")) {
            cout << "The tunnel lights up. You see a hidden door!\n";
        } else {
            cout << "In the dark, you stumble and hurt yourself.\n";
            cout << "[Game Over]\n";
            return 0;
        }
    } else {
        cout << "\nYou climb the stairs and reach a heavy door.\n";
    }

    // --- Second decision: handled by switch ---
    cout << "\nBeyond the door, a monster blocks your way!\n";
    cout << "What do you do?\n";
    cout << "  1) Fight with your bare hands\n";
    cout << "  2) Try to distract it\n";
    cout << "  3) Run for the exit\n";
    int monsterChoice = getChoice(1, 3);

    switch (monsterChoice) {
        case 1:
            cout << "You bravely fight, but the monster is too strong.\n";
            cout << "[Game Over]\n";
            break;
        case 2:
            cout << "You throw a rock to distract it and slip past.\n";
            cout << "[You Escaped!]\n";
            break;
        case 3:
            cout << "You sprint past the monster into the fresh night air.\n";
            cout << "[You Escaped!]\n";
            break;
        default:
            cout << "You freeze in fear. The monster catches you.\n";
            cout << "[Game Over]\n";
    }

    return 0;
}
