    public class JvmComprehension {

        public static void main(String[] args) {
            int i = 1;                      // 1
            Object o = new Object();        // 2
            Integer ii = 2;                 // 3
            printAll(o, i, ii);             // 4
            System.out.println("finished"); // 7
        }
    
        private static void printAll(Object o, int i, Integer ii) {
            Integer uselessVar = 700;                   // 5
            System.out.println(o.toString() + i + ii);  // 6
        }
    }


1. Создается переменная i типа int и ей присваивается значение 1. Эта переменная создается на стэке, в фрейме метода main.
2. Создается новый объект класса Object и переменной o присваивается ссылка на него. Объект создается в куче, 
выделяется память для его полей и методов, а переменная o создается на стэке в том же фрейме, что и переменная i.
3. Создается объект класса Integer со значением 2 и переменной ii присваивается ссылка на него. 
Объект создается в куче, а переменная ii создается на стэке в том же фрейме, что и переменные i и o.
4. Вызывается метод printAll с аргументами o, i и ii. Создается новый фрейм на стэке для метода printAll, 
в который копируются аргументы из фрейма метода main. Переменные o и ii передаются по ссылке - их значение не копируется,
а i передается по значению, для нее создается копия в фрейме printAll.
5. Создается переменная uselessVar типа Integer и ей присваивается значение 700. Эта переменная создается на стэке, 
в фрейме метода printAll.
6. Вызывается метод toString() объекта o, который возвращает строковое представление объекта. Затем к этой строке 
конкатенируются значения переменных i и ii. Результат выводится на экран. Все это происходит в фрейме метода printAll, 
на стэке.
7. Метод printAll завершается, его фрейм удаляется со стэка. Контроль возвращается в метод main, на стэке остаются
переменные i, o и ii.

При выполнении данного кода в JVM используются области памяти: стэк и куча. Переменные i, o и ii создаются на стэке, 
а объекты o и ii создаются в куче.

Также используется сборщик мусора, который удаляет объекты, на которые нет ссылок из переменных в стэке или других 
объектов в куче. Например, после завершения работы метода printAll переменная uselessVar удаляется из стэка, а объект, 
на который ссылается переменная o, остается в куче, пока существует ссылка на него.

ClassLoader'ы в данном коде не исопльзуются