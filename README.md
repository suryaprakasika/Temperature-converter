# Temperature-converter
This project focuses on developing a simple and efficient Temperature Converter that allows users to convert values between Celsius, Fahrenheit, and Kelvin. 
import java.util.*;



// ===============================

// CO5 → Interface for Conversion

// ===============================

interface Converter {

    double toCelsius(double value);

    double toFahrenheit(double value);

    double toKelvin(double value);

}



// ===================================================

// CO4 & CO5 → Parent Class (OOP + Encapsulation)

// ===================================================

abstract class Temperature implements Converter {

    protected double value;



    public Temperature(double value) {

        this.value = value;

    }

}



// ===============================================

// CO5 → Child Classes (Inheritance + Polymorphism)

// ===============================================



class Celsius extends Temperature {

    public Celsius(double value) { super(value); }



    public double toCelsius(double v) { return v; }

    public double toFahrenheit(double v) { return (v * 9/5) + 32; }

    public double toKelvin(double v) { return v + 273.15; }

}



class Fahrenheit extends Temperature {

    public Fahrenheit(double value) { super(value); }



    public double toCelsius(double v) { return (v - 32) * 5/9; }

    public double toFahrenheit(double v) { return v; }

    public double toKelvin(double v) { return ((v - 32) * 5/9) + 273.15; }

}



class Kelvin extends Temperature {

    public Kelvin(double value) { super(value); }



    public double toCelsius(double v) { return v - 273.15; }

    public double toFahrenheit(double v) { return ((v - 273.15) * 9/5) + 32; }

    public double toKelvin(double v) { return v; }

}





// ========================================================

// CO6 → Using Collections + Exception Handling + Modularity

// ========================================================



public class TemperatureConverterApp {



    // CO3 → Simple recursion for menu repeat

    public static void showMenu() {

        Scanner sc = new Scanner(System.in);



        System.out.println("\n===== TEMPERATURE CONVERTER =====");

        System.out.print("Enter value: ");



        try {

            double value = sc.nextDouble();



            System.out.print("Enter unit (C/F/K): ");

            char unit = sc.next().toUpperCase().charAt(0);



            Temperature tempObj;



            switch(unit) {

                case 'C': tempObj = new Celsius(value); break;

                case 'F': tempObj = new Fahrenheit(value); break;

                case 'K': tempObj = new Kelvin(value); break;

                default:

                    throw new IllegalArgumentException("Invalid unit!");

            }



            // CO2 → Using an array to store converted values

            double[] results = {

                tempObj.toCelsius(value),

                tempObj.toFahrenheit(value),

                tempObj.toKelvin(value)

            };



            // CO6 → Storing results using Collections

            List<String> output = new ArrayList<>();

            output.add("Celsius: " + results[0]);

            output.add("Fahrenheit: " + results[1]);

            output.add("Kelvin: " + results[2]);



            System.out.println("\nConverted Values:");

            for (String s : output) System.out.println(s);



        } catch (Exception e) {

            System.out.println("Error: " + e.getMessage());

        }



        // Recursion to continue

        System.out.print("\nConvert again? (y/n): ");

        char ch = sc.next().charAt(0);

        if (ch == 'y' || ch == 'Y') showMenu();

        else System.out.println("Thank you!");

    }



    // CO1 → Main method with basic program flow

    public static void main(String[] args) {

        showMenu();

    }

}
