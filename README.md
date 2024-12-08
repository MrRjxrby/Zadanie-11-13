# Zadanie-11-13
Задание 11.1
```
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);


        String dSup = "Кочкин"; 

        System.out.print("Введите дату и время получения задания (формат: ГГГГ-ММ-ДД ЧЧ:ММ:СС): ");
        String inputDate = scanner.nextLine();

        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date dTake = null;

        try {
            dTake = dateFormat.parse(inputDate);
        } catch (ParseException e) {
            System.out.println("Ошибка при вводе даты. Пожалуйста, введите в правильном формате.");
            scanner.close();
            return;
        }

        try {
            Thread.sleep(1000); // Задержка в 1 секунд
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        Date dSub = new Date(); // Время сдачи задания

        // Вывод информации
        System.out.println("Фамилия разработчика: " + dSup);
        System.out.println("Дата и время получения задания: " + dTake);
        System.out.println("Дата и время сдачи задания: " + dSub);

        scanner.close();
    }
}
```
Задание 11.2
```
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class DateComparison {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MM-yyyy");
        dateFormat.setLenient(false);

        Date currentDate = new Date(); //текущая дата

        System.out.println("Текущая дата: " + dateFormat.format(currentDate));

        System.out.print("Введите дату для сравнения (формат ГГГГ-ММ-ДД): ");
        String inputDate = scanner.nextLine();

        try {
            Date userDate = dateFormat.parse(inputDate);

            if (userDate.before(currentDate)) {
                System.out.println("Введенная дата " + inputDate + " находится в прошлом.");
            } else if (userDate.after(currentDate)) {
                System.out.println("Введенная дата " + inputDate + " находится в будущем.");
            } else {
                System.out.println("Введенная дата " + inputDate + " совпадает с текущей датой.");
            }
        } catch (ParseException e) {
            System.out.println("Ошибка: некорректный формат даты. Пожалуйста, введите дату в формате ГГГГ-ММ-ДД.");
        } finally {
            scanner.close();
        }
    }
}
```
Задание 13.4
```
import java.util.ArrayList;
import java.util.List;

class Shirt {
    private String id;
    private String name;
    private String color;
    private String size;

    public Shirt(String id, String name, String color, String size) {
        this.id = id;
        this.name = name;
        this.color = color;
        this.size = size;
    }

    // Переопределение метода toString()
    @Override
    public String toString() {
        return "ИД: " + id + "\n" +
               "Название: " + name + "\n" +
               "Цвет: " + color + "\n" +
               "Размер: " + size + "\n" +
               "----------------------------";
    }
}

public class Main {
    public static void main(String[] args) {
        String[] shirts = {
            "S001,Black Polo Shirt,Black,XL",
            "S002,Black Polo Shirt,Black,L",
            "S003,Blue Polo Shirt,Blue,XL",
            "S004,Blue Polo Shirt,Blue,M",
            "S005,Tan Polo Shirt,Tan,XL",
            "S006,Black T-Shirt,Black,XL",
            "S007,White T-Shirt,White,XL",
            "S008,White T-Shirt,White,L",
            "S009,Green T-Shirt,Green,S",
            "S010,Orange T-Shirt,Orange,S",
            "S011,Maroon Polo Shirt,Maroon,S"
        };

        List<Shirt> shirtList = new ArrayList<>();

        for (String shirtString : shirts) {
            String[] shirtDetails = shirtString.split(",");
            Shirt shirt = new Shirt(shirtDetails[0], shirtDetails[1], shirtDetails[2], shirtDetails[3]);
            shirtList.add(shirt);
        }

        for (Shirt shirt : shirtList) {
            System.out.println(shirt);
        }
    }
}
```
Задание 13.5
```
public class Main {
    private String countryCode;
    private String formattedNumber;

    public Main(String phoneNumber) {
        if (phoneNumber.startsWith("+")) {
            processInternationalFormat(phoneNumber);
        } else if (phoneNumber.startsWith("8")) {
            processDomesticFormat(phoneNumber);
        } else {
            throw new IllegalArgumentException("Неверный формат телефонного номера");
        }
    }

    private void processInternationalFormat(String phoneNumber) {
        String numberWithoutPlus = phoneNumber.substring(1);
        this.countryCode = numberWithoutPlus.substring(0, numberWithoutPlus.length() - 10);
        String mainNumber = numberWithoutPlus.substring(numberWithoutPlus.length() - 10); // последние 10 цифр
        this.formattedNumber = formatNumber(mainNumber);
    }

    private void processDomesticFormat(String phoneNumber) {
        String mainNumber = phoneNumber.substring(1); // оставшиеся 10 цифр
        this.countryCode = "7"; // код страны для России
        this.formattedNumber = formatNumber(mainNumber);
    }

    private String formatNumber(String number) {
        return number.substring(0, 3) + "-" + number.substring(3, 6) + "-" + number.substring(6);
    }

    @Override
    public String toString() {
        return "+" + countryCode + " " + formattedNumber;
    }

    public static void main(String[] args) {
        String[] testNumbers = { "+79175655655", "+104289652211", "89175655655" };

        for (String testNumber : testNumbers) {
            Main phoneNumber = new Main(testNumber);
            System.out.println(phoneNumber);
        }
    }
}
```
