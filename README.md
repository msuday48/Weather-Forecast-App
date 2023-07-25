import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class SWAPING {

    private static final String API_KEY = "b6907d289e10d714a6e88b30761fae22";
    private static final String BASE_URL = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=" + API_KEY;

    public static void main(String[] args) {
        try {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            String input;

            while (true) {
                System.out.println("\nOptions:");
                System.out.println("1. Get weather");
                System.out.println("2. Get Wind Speed");
                System.out.println("3. Get Pressure");
                System.out.println("0. Exit");
                System.out.print("Enter your choice: ");
                input = br.readLine();

                switch (input) {
                    case "1":
                        System.out.print("Enter the date (YYYY-MM-DD): ");
                        String date1 = br.readLine();
                        printWeather(date1);
                        break;
                    case "2":
                        System.out.print("Enter the date (YYYY-MM-DD): ");
                        String date2 = br.readLine();
                        printWindSpeed(date2);
                        break;
                    case "3":
                        System.out.print("Enter the date (YYYY-MM-DD): ");
                        String date3 = br.readLine();
                        printPressure(date3);
                        break;
                    case "0":
                        System.out.println("Exiting the program.");
                        return;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static String fetchDataFromAPI() throws IOException {
        URL url = new URL(BASE_URL);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");

        StringBuilder response = new StringBuilder();
        try (BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()))) {
            String line;
            while ((line = br.readLine()) != null) {
                response.append(line);
            }
        } finally {
            conn.disconnect();
        }
        return response.toString();
    }

    private static void printWeather(String date) throws IOException {
        String jsonData = fetchDataFromAPI();
      
        System.out.println("Weather data for " + date + ": " + jsonData);
    }

    private static void printWindSpeed(String date) throws IOException {
        String jsonData = fetchDataFromAPI();
       
        System.out.println("Wind speed data for " + date + ": " + jsonData);
    }

    private static void printPressure(String date) throws IOException {
        String jsonData = fetchDataFromAPI();
       
        System.out.println("Pressure data for " + date + ": " + jsonData);
    }
}
