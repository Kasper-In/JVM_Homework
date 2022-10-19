## Работа JVM

```java
public class JvmComprehension {          
    public static void main(String[] args) {
        int i = 1;                      // 1 В Metaspace загружается класс JvmComprehension с помощью ClassLoader
                                        // В Stack Memory во фрейме main класса JvmComprehension создаётся переменная i типа int  
                                        // Ей присваивается значение 1;

        Object o = new Object();        // 2 В Stack Memory во фрейме main класса JvmComprehension создаётся переменная Object 
                                        // В Heap создаётся объект типа Object, на который ссылается переменная Object;

        Integer ii = 2;                 // 3 В Stack Memory во фрейме main класса JvmComprehension создаётся переменная i2 со значение 2
                                        // В Heap создаётся объект типа Interger, на который ссылается переменная i2;

        printAll(o, i, ii);             // 4 В Stack Memory создаётся фрейм printAll;

        System.out.println("finished"); // 7 В Stack Memory создаётся фрейм println, принимающий ссылку типа String на 
                                        // объект из Heap со значением "finished"
                                        // По завершении метода main (программы) сборщик мусора удалит объекты из кучи и фреймы из стека
    }

    private static void printAll(Object o, int i, Integer ii) {
                                        // 5 В Stack Memory во фрейме printAll класса JvmComprehension создаётся переменные о, i и i1
                                        // В Heap создаётся объект типа Interger, на который ссылается переменная i2, и объект типа Object, на который ссылается переменная o
        Integer uselessVar = 700;       // В Stack Memory во фрейме printAll класса JvmComprehension создаётся переменная uselessVar со значением 700
                                        // В Heap создаётся объект типа Interger, на который ссылается переменная uselessVar;           

        System.out.println(o.toString() + i + ii);  // 6 В Stack Memory создаётся фрейм println с переменными o, i, ii
                                                    // каждая переменная создаёт свой фрейм toString
                                                    // Полученная строка сохраняется в Heap, на которую будет ссылаться переменная типа String во фрейме println в Stack Memory
                                                    // После заверщения работы метода сборщик мусора удаляет:
                                                    //    - фреймы toString переменных, 
                                                    //    - фрейм println с объектами Object и Interger, переменной  i,
                                                    //    - объект, хранящий результат сложения строк.               
    }
}

```
