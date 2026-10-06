import java.util.Scanner;

/**
 * THE MISSING EXAM PAPER - Detective Investigation System
 * Single-file version: all classes are in this one file.
 *
 * Compile : javac DetectiveGame.java
 * Run     : java DetectiveGame
 */

// ---------------------------------------------------------------
// Suspect : stores the details of one suspect
// ---------------------------------------------------------------
class Suspect {

    private int id;
    private String name;
    private String location;
    private String alibi;

    // Constructor (uses the 'this' keyword)
    public Suspect(int id, String name, String location, String alibi) {
        this.id = id;
        this.name = name;
        this.location = location;
        this.alibi = alibi;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getLocation() {
        return location;
    }

    public String getAlibi() {
        return alibi;
    }

    // Display the details of ONE suspect
    public void displayDetails() {
        System.out.println("ID       : " + id);
        System.out.println("Name     : " + name);
        System.out.println("Location : " + location);
        System.out.println("Alibi    : " + alibi);
    }

    // Create the five suspects and store them in an array
    public static Suspect[] createSuspects() {
        Suspect[] suspects = new Suspect[5];
        suspects[0] = new Suspect(1, "Alex", "Computer Lab", "Working on a project");
        suspects[1] = new Suspect(2, "Maya", "Library", "Studying");
        suspects[2] = new Suspect(3, "Rahul", "Staff Room", "Meeting a faculty member");
        suspects[3] = new Suspect(4, "Sara", "Canteen", "Having lunch");
        suspects[4] = new Suspect(5, "Arjun", "Department Office", "Collecting documents");
        return suspects;
    }

    // Display ALL suspects (for-each loop)
    public static void displayAllSuspects(Suspect[] suspects) {
        System.out.println("---------- SUSPECTS ----------");
        for (Suspect s : suspects) {
            s.displayDetails();
            System.out.println("------------------------------");
        }
    }
}

// ---------------------------------------------------------------
// ClueManager : stores clues and tracks which are collected
// ---------------------------------------------------------------
class ClueManager {

    private String[] clues = {
        "The office door was opened at 2:15 PM.",
        "CCTV shows someone entering the office.",
        "A torn piece of paper was found near the printer.",
        "A suspect's ID card was found inside the office.",
        "The printer was used shortly before the question paper disappeared."
    };

    // collected[i] is true when clues[i] has been collected
    private boolean[] collected = new boolean[clues.length];

    public int getTotalClues() {
        return clues.length;
    }

    // Display all available clues and whether each is collected
    public void displayAvailableClues() {
        System.out.println("-------- AVAILABLE CLUES --------");
        for (int i = 0; i < clues.length; i++) {
            String status = collected[i] ? "[Collected]" : "[Not collected]";
            System.out.println((i + 1) + ". " + clues[i] + " " + status);
        }
        System.out.println("---------------------------------");
    }

    // Collect a clue by number (1 to 5). Returns true if newly collected.
    public boolean collectClue(int clueNumber) {
        if (clueNumber < 1 || clueNumber > clues.length) {
            System.out.println("Invalid clue number: " + clueNumber);
            return false;
        }

        int index = clueNumber - 1;

        if (collected[index]) {
            System.out.println("Clue " + clueNumber + " has already been collected.");
            return false;
        }

        collected[index] = true;
        System.out.println("Clue " + clueNumber + " collected: " + clues[index]);
        return true;
    }

    // Display all clues collected so far
    public void displayCollectedClues() {
        System.out.println("-------- COLLECTED CLUES --------");
        int count = 0;
        for (int i = 0; i < clues.length; i++) {
            if (!collected[i]) {
                continue;
            }
            count++;
            System.out.println((i + 1) + ". " + clues[i]);
        }
        if (count == 0) {
            System.out.println("No clues have been collected yet.");
        }
        System.out.println("---------------------------------");
    }

    public int getCollectedCount() {
        int count = 0;
        for (boolean c : collected) {
            if (c) {
                count++;
            }
        }
        return count;
    }
}

// ---------------------------------------------------------------
// Investigation : suspect search + accusation logic (3 attempts)
// ---------------------------------------------------------------
class Investigation {

    private static final int MAX_ATTEMPTS = 3;

    private Suspect[] suspects;
    private int culpritId;          // hidden from the detective
    private int attemptsUsed;
    private boolean caseClosed;
    private boolean caseSolved;

    public Investigation(Suspect[] suspects, int culpritId) {
        this.suspects = suspects;
        this.culpritId = culpritId;
        this.attemptsUsed = 0;
        this.caseClosed = false;
        this.caseSolved = false;
    }

    // Find a suspect by ID; returns null if not found
    public Suspect findSuspect(int suspectId) {
        for (int i = 0; i < suspects.length; i++) {
            if (suspects[i].getId() == suspectId) {
                return suspects[i];
            }
        }
        return null;
    }

    // Show the details of the chosen suspect
    public void investigateSuspect(int suspectId) {
        Suspect s = findSuspect(suspectId);

        if (s == null) {
            System.out.println("No suspect found with ID " + suspectId + ".");
        } else {
            System.out.println("-------- SUSPECT DETAILS --------");
            s.displayDetails();
            System.out.println("---------------------------------");
        }
    }

    // Make ONE accusation. Returns true only if the culprit is identified.
    public boolean accuse(int suspectId) {
        if (caseClosed) {
            System.out.println("The case is already closed.");
            return caseSolved;
        }

        Suspect accused = findSuspect(suspectId);
        if (accused == null) {
            System.out.println("No suspect found with ID " + suspectId
                    + ". This does not count as an attempt.");
            return false;
        }

        attemptsUsed++;
        System.out.println("You accuse " + accused.getName()
                + " (Attempt " + attemptsUsed + " of " + MAX_ATTEMPTS + ")");

        if (accused.getId() == culpritId) {
            System.out.println();
            System.out.println("CASE SOLVED!");
            System.out.println("You identified the culprit.");
            System.out.println("The missing question paper has been recovered.");
            caseClosed = true;
            caseSolved = true;
            return true;
        }

        int remaining = MAX_ATTEMPTS - attemptsUsed;
        if (remaining == 0) {
            System.out.println();
            System.out.println("INVESTIGATION FAILED!");
            System.out.println("You have used all three attempts.");
            System.out.println("The culprit escaped.");
            caseClosed = true;
        } else {
            System.out.println("Wrong accusation! " + accused.getName()
                    + " is not the culprit. Attempts remaining: " + remaining);
        }
        return false;
    }

    public boolean isCaseClosed() {
        return caseClosed;
    }

    public boolean isCaseSolved() {
        return caseSolved;
    }

    public int getAttemptsUsed() {
        return attemptsUsed;
    }
}

// ---------------------------------------------------------------
// DetectiveGame : main program, menu and program flow
// ---------------------------------------------------------------
public class DetectiveGame {

    static void displayMenu() {
        System.out.println();
        System.out.println("=================================");
        System.out.println("     DETECTIVE INVESTIGATION");
        System.out.println("=================================");
        System.out.println("1. View Suspects");
        System.out.println("2. Investigate Suspect");
        System.out.println("3. Collect Clue");
        System.out.println("4. View Collected Clues");
        System.out.println("5. Accuse Suspect");
        System.out.println("6. Exit");
        System.out.println("=================================");
    }

    // Read an integer from the user. Keeps asking until a number is typed.
    // Returns -1 if there is no more input (e.g. input stream closed).
    static int readInt(Scanner sc, String prompt) {
        while (true) {
            System.out.print(prompt);
            if (!sc.hasNextLine()) {
                return -1;
            }
            String line = sc.nextLine().trim();
            try {
                return Integer.parseInt(line);
            } catch (NumberFormatException e) {
                System.out.println("Please enter a valid number.");
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Create the objects required by the program
        Suspect[] suspects = Suspect.createSuspects();
        ClueManager clueManager = new ClueManager();

        // The actual culprit (ID 5) is hidden inside Investigation
        Investigation investigation = new Investigation(suspects, 5);

        System.out.println("The exam question paper has disappeared from the department office!");
        System.out.println("Five students were present. Find the culprit, Detective.");

        boolean running = true;

        while (running) {
            displayMenu();
            int choice = readInt(sc, "Enter your choice (1-6): ");

            if (choice == -1) {
                System.out.println();
                System.out.println("No more input. Exiting the investigation.");
                break;
            }

            switch (choice) {
                case 1:
                    Suspect.displayAllSuspects(suspects);
                    break;

                case 2: {
                    int suspectId = readInt(sc, "Enter suspect ID (1-5) to investigate: ");
                    investigation.investigateSuspect(suspectId);
                    break;
                }

                case 3: {
                    clueManager.displayAvailableClues();
                    int clueNo = readInt(sc, "Enter clue number (1-5) to collect: ");
                    clueManager.collectClue(clueNo);
                    break;
                }

                case 4:
                    clueManager.displayCollectedClues();
                    break;

                case 5: {
                    int accusedId = readInt(sc, "Enter suspect ID (1-5) to accuse: ");
                    investigation.accuse(accusedId);
                    if (investigation.isCaseClosed()) {
                        running = false;   // case solved or all attempts used
                    }
                    break;
                }

                case 6:
                    System.out.println("Exiting the investigation. Goodbye, Detective!");
                    running = false;
                    break;

                default:
                    System.out.println("Invalid option. Please choose a number from 1 to 6.");
                    continue;
            }
        }

        // Final summary
        System.out.println();
        System.out.println("========== INVESTIGATION SUMMARY ==========");
        System.out.println("Clues collected    : " + clueManager.getCollectedCount()
                + " of " + clueManager.getTotalClues());
        System.out.println("Accusation attempts: " + investigation.getAttemptsUsed() + " of 3");
        System.out.println("Case solved        : " + (investigation.isCaseSolved() ? "Yes" : "No"));
        System.out.println("===========================================");

        sc.close();
    }
}
