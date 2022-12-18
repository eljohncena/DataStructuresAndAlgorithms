import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;
import java.util.TreeMap;

public class CapitalProgram {

	public static void main (String[] args) {
		
		// 2D-Array of States and Capitals ordered by State 
		String[][] capitalState = {
				{"Alabama", "Alaska", "Arizona", "Arkansas", "California",
					"Colorado", "Connecticut", "Delaware", "Florida", "Georgia",
					"Hawaii", "Idaho", "Illinois", "Indiana", "Iowa", "Kansas",
					"Kentucky", "Louisiana", "Maine", "Maryland", "Massachusetts",
					"Michigan", "Minnesota", "Mississippi", "Missouri", "Montana",
					"Nebraska", "Nevada", "New Hampshire", "New Jersey",
					"New Mexico", "New York", "North Carolina", "North Dakota",
					"Ohio", "Oklahoma", "Oregon", "Pennsylvania", "Rhode Island",
					"South Carolina", "South Dakota", "Tennessee", "Texas", "Utah",
					"Vermont", "Virginia", "Washington", "West Virginia",
					"Wisconsin", "Wyoming"},
                {"Montgomery", "Juneau", "Phoenix", "Little Rock", "Sacramento",
						"Denver", "Hartford", "Dover", "Tallahassee", "Atlanta",
						"Honolulu", "Boise", "Springfield", "Indianapolis",
						"Des Moines", "Topeka", "Frankfort", "Baton Rouge", "Augusta",
						"Annapolis", "Boston", "Lansing", "Saint Paul", "Jackson",
						"Jefferson City", "Helena", "Lincoln", "Carson City", "Concord",
						"Trenton", "Santa Fe", "Albany", "Raleigh", "Bismarck",
						"Columbus", "Oklahoma City", "Salem", "Harrisburg", "Providence",
						"Columbia", "Pierre", "Nashville", "Austin", "Salt Lake City",
						"Montpelier", "Richmond", "Olympia", "Charleston", "Madison", "Cheyenne"}
		};
		
		System.out.println("Welcome to the Capital State Game!");
		System.out.println("\n");
		
		Scanner scanner = new Scanner(System.in);
		
		//Prompt user to enter capital
		System.out.println("Enter a Capital");	
		String currentAnswer = scanner.nextLine();
		
		//Variable initialized to begin loop to compare.
		boolean correct = false;
		
		//Sub-Array of Capitals to check if user answer is within Sub-array.
		String[] capitals = capitalState[1];
		
		for (String city : capitals) {
			if (city.equalsIgnoreCase(currentAnswer)) {
				correct = true;
				System.out.println("Correct!, " + currentAnswer + " is a State Capital.");
				System.out.println("\n");
				break;
			}
		}
		
		if(correct == false){
			System.out.println("Sorry, " + currentAnswer + " is not a State Capital.");
			System.out.println("\n");
		}
		
		// Print Array
		System.out.println("Now printing Capitals and which State they belong to.");
		System.out.println("\n");
		for(int i = 0; i < capitalState[0].length; i++) {
			System.out.println("The captal of " + capitalState[0][i] + " is " + capitalState[1][i]);
			
		}
		//Begin Sort
		System.out.println("\n");
		System.out.println("Rearranging array by Capital:");
		System.out.println("\n");
		//Two nested loops to sort array by Capital
		for (int i = 0; i < capitalState[0].length; i++) {
			for (int j = i + 1; j < capitalState[0].length; j++) {
				String city;
				String state;
				
				if(capitalState[1][j].compareTo(capitalState[1][i]) < 0) {
					
					city = capitalState[1][i];
					capitalState[1][i] = capitalState[1][j];
					capitalState[1][j] = city;
					
					state = capitalState[0][i];
					capitalState[0][i] = capitalState[0][j];
					capitalState[0][j] = state;
					
					
				}
			}
		}
		
		for(int i = 0; i < capitalState[0].length; i++) {
			System.out.println("The captal of " + capitalState[0][i] + " is " + capitalState[1][i]);
			
		}
		
		//Beginning of Game to ask capitals of each statee
		System.out.println("\n");
		System.out.println("Now lets play a little game...");
		System.out.println("You will be prompted to enter the Capital that belongs to each State.");
		System.out.println("Enter quit to exit game");
		System.out.println("\n");
		
		Scanner gameScanner = new Scanner(System.in);
		boolean endGame = false;
		int correctAnswerCount = 0;
		int wrongAnswerCount = 0;
		ArrayList<String> userInput = new ArrayList<>();
		
		
		//Loop will go through each State and ask for its capital. 
		while(!endGame) {
			
			//Begin of loop.
			for(int i = 0; i < capitalState[0].length; i++) {
				System.out.println("The captal of " + capitalState[0][i] + " is?");
				String gameAnswer = gameScanner.nextLine();
				
				//Will exit program if quit is entered. 
				if(gameAnswer.equalsIgnoreCase("quit")) {
					System.out.println("Quitting Game.");
					System.out.println("You have quit the game. Total correct answers: " + correctAnswerCount);
					System.out.println("Total incorrect answers: " + wrongAnswerCount);
					endGame = true;
					break;
				}
				else {
					userInput.add(gameAnswer);
					
					//Will increase counter if answer is correct or wrong.
					if(capitalState[1][i].equalsIgnoreCase(gameAnswer)){
						correctAnswerCount += 1;
						System.out.println("Correct!");
					}
					else {
						System.out.println("Wrong Answer!");
						wrongAnswerCount += 1;
					}
				}
			}
			System.out.println("The game has ended");
			System.out.println("\n");
			endGame = true;
		}
		
		//Create HashMap to sort array
		HashMap<String,String> capitalStateHashMap = new HashMap<>(capitalState[0].length);

		//Add items to HashMap
		for(int i = 0; i < capitalState[0].length; i++) {
			
			capitalStateHashMap.put(capitalState[0][i], capitalState[1][i]);
		}
		
		//Print the HashMap
		System.out.println("The HashMap size is " + capitalStateHashMap.size());
		System.out.println("The key value pairs are: ");
		
		for (String key: capitalStateHashMap.keySet()) {
			System.out.println("The capital of " + key + " is " + capitalStateHashMap.get(key));
		}
		
		//Use a TreeMap to sort using a binary search tree for storage.
		TreeMap<String, String> capitalStateTreeSorted = new TreeMap<>(capitalStateHashMap);
		
		//Now program will ask user for State and program will display the corresponding Capital
		System.out.println("Now we will ask you to enter a state and the program will display the corresponding capital.");
		System.out.println("Enter quit to exit program");
		
		endGame = false;
		while(!endGame) {
			System.out.println("Please enter a State");
			String gameLoopInput = gameScanner.nextLine();
			
			if(gameLoopInput.equalsIgnoreCase("quit")) {
				System.out.println("The game is now exiting.");
				endGame = true;
				break;
			}
			else if(capitalStateTreeSorted.containsKey(gameLoopInput)) {
				System.out.println("The capital of " + gameLoopInput + " is " + capitalStateTreeSorted.get(gameLoopInput));
			}
			else {
				System.out.println("Input not found. Please try again or enter quit to exit.");
			}
			
		}
		
		System.out.println("Thanks for playing!");
	}	
}
