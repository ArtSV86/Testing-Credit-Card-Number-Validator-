**Отчёт о тестировании "Credit Card Number Validator"**

Краткое описание

<08.03.2021> - <08.03.2021> было проведено <сантираное тестирование(sanity testing)> приложения 
"Credit Card Number Validator".

На тестирование затрачено: <0,2 часа>

**В результате тестирования выявлены следующие дефекты:**

    <https://github.com/ArtSV86/OpenJDK11-KeyValidator/issues/1>


**Описание процесса тестирования**

В процессе тестирования использовались следующие артефакты:
* <Main.java>
* тестовый сценарий "Credit Card Number Validator"

**Тестовый сценарий для "Credit Card Number Validator":**
* Шаг 1. Открыть файл Main.java в IntelliJ IDEA, содержащий код:

```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
* Шаг 2. В строке кода **String number = "5351719427810741"** ввести тестируемое значение "номер карты":

VISA:
* 4024007138330410827

American Express (AMEX):
* 349871709298008
* 340314936131642
* 347217113704664

Discover:    
* 6011529282212134982

JCB:
* 3538293422775661166



В качестве тестовых данных использовались данные <https://www.freeformatter.com/credit-card-number-generator-validator.html>:

**Ожидаемые валидные данные(номера карт) после проверки**
    

    VISA:
    4024007138330410827
    American Express (AMEX):
    349871709298008
    340314936131642
    347217113704664
    Discover:
    6011529282212134982
    JCB:
    3538293422775661166



**Тестирование производилось в следующем окружении:**

    <Windows 10, 64 bit>
    <версия Java "11.0.10">
    <ПО: IntelliJ IDEA Community Edition>
