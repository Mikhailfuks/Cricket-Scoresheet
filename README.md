#include <iostream>
#include <vector>
#include <string>

class Player {
public:
    Player(const std::string& name) : name(name), runs(0) {}

    void addRuns(int run) {
        runs += run;
    }

    std::string getName() const {
        return name;
    }

    int getRuns() const {
        return runs;
    }

private:
    std::string name;
    int runs;
};

class Team {
public:
    void addPlayer(const std::string& playerName) {
        players.push_back(Player(playerName));
    }

    void recordRuns(const std::string& playerName, int run) {
        for (auto& player : players) {
            if (player.getName() == playerName) {
                player.addRuns(run);
                return;
            }
        }
        std::cout << "Player not found!" << std::endl;
    }

    void displayScorecard() const {
        std::cout << "\n--- Scorecard ---" << std::endl;
        for (const auto& player : players) {
            std::cout << player.getName() << ": " << player.getRuns() << " runs" << std::endl;
        }
    }

    int getTotalRuns() const {
        int total = 0;
        for (const auto& player : players) {
            total += player.getRuns();
        }
        return total;
    }

private:
    std::vector<Player> players;
};

int main() {
    Team team;
    int choice;

    while (true) {
        std::cout << "\n=== Cricket Scoresheet ===" << std::endl;
        std::cout << "1. Add Player" << std::endl;
        std::cout << "2. Record Runs" << std::endl;
        std::cout << "3. Display Scorecard" << std::endl;
        std::cout << "4. Display Total Runs" << std::endl;
        std::cout << "5. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::string playerName;
                std::cout << "Enter player name: ";
                std::cin >> ws;  // Discard leading whitespace
                std::getline(std::cin, playerName);
                team.addPlayer(playerName);
                std::cout << "Player added successfully!" << std::endl;
                break;
            }
            case 2: {
                std::string playerName;
                int runs;
                std::cout << "Enter player name: ";
                std::cin >> ws;  // Discard leading whitespace
                std::getline(std::cin, playerName);
                std::cout << "Enter runs scored: ";
                std::cin >> runs;
                team.recordRuns(playerName, runs);
                break;
            }
            case 3:
                team.displayScorecard();
                break;
            case 4:
                std::cout << "Total Runs: " << team.getTotalRuns() << std::endl;
                break;
            case 5:
                std::cout << "Exiting..." << std::endl;
                return 0;
            default:
                std::cout << "Invalid choice! Please try again." << std::endl;
        }
    }

    return 0;
}
