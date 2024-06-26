# Вопросы

# *Базовые* вопросы

### 1. Какие виды пользовательских типов существуют в языке?

### 2. Что такое сигнатура функции? Какой тип имеет имя функции?

### 3. Вам даны два сегмента кода, объясните какой из них корректен и почему.

```cpp
// (1)
void f() {
	void g() {
		// ...
	}
}

// (2)
void g() {
	auto f = []() {
		// ...
	};
}
```

### 4. Какие существуют спецификаторы у функций? У методов класса?

### 5. Вам дан сегмент кода. Какие будут результаты, если скомпилировать его с помощью `g++ -x c++ main` и `gcc -x c main` ?

```cpp
void f(int a) {
	// ...
}

void f(bool b) {
	// ...
}

int main(int, char**) {
    f(1);
    f(false);
}
```

### 6. Вам дан фрагмент кода. Его скомпилировали с флагом `-O2` и запустили. Каким был вывод программы? Что будет если поменять `int` на `unsigned int` ?

```cpp
void f() {
    for (int i = 0; i < 100; ++i) {
        std::cout << i << ' ' << i * 100000000 << std::endl;
    }
}
```

### 7. Определите размер предложенного `union`? Что будет если поменять `N` на 5? Какие ограничения накладываются на поля `union`?

```cpp
constexpr int N = 4;

union U {
    int a;
    char b;
    short c[N];
};
```

### 8. Вам дан отрывок кода. Какими будут размеры объявленных структур?

```cpp
struct A {};

struct B {
    void* p;
};

struct C {
    int a: 13;
    int b: 19;
};
```

### 9. Что такое SEGFAULT и можно ли его поймать с помощью `catch`? Какова его первопричина?

### 10. Каким будет результат компиляции следующего кода?

```cpp
void f() {
	delete (int*) nullptr;
}
```

### 11. В чем различия поведения программы и памяти полученной следующими сегментами кода?

```cpp
struct Char {
    char c;
    Char() : c(0) {}
};

int main() {
    // (1)
    auto p1 = std::malloc(5);
    
    // (2)
    auto p2 = new Char[5];
}
```

# STD

Следующие вопросы относятся к стандартной библиотеке C++. Ответами на некоторые вопросы может являться название какого-то члена *std* 😉

### 12. Решение проблемы *dangling pointer* и *memory leak*.

### 13. Как хранить данные разных типов в одной переменной?

### 14. Проблема `throw`. Иной способ возвращать ошибки.

### 15. Как устроено хранение элементов `std::vector<bool>` ?

### 16. Может быть `std::optional`.

### 17. *Самый умный?* Что делает `std::move` ?

### 18. Расскажите про библиотечки `<bit>`, `<span>`, `<ranges>`.

# Конечные вопросы

### 19. Что делает ключевое слово `decltype`? В чем разница `decltype(a)` и `decltype((a))` ?

### 20. Что делает `(void)x` ?

### 21. Что нужно, чтобы код `for(T x; auto p : x)` был валиден?

### 22. Скомпилируется ли следующий код и в чем его смысл?

```cpp
[[noreturn]]
void f() {
    // ...
}
```

### 23. В какой код скомпилируется следующая функция? И что произойдет, если ее вызвать?

```cpp
#include <utility>

void f() {
    volatile int x = 1;
    if (x % 2 == 0)
        return;
    std::unreachable();
}
```

### 24. Назовите все случаи, когда в коде программы может встречаться `...` (7 случаев).

- `void f(...)`
- `#define f(...)`
- `catch (...)`
- `template<class... Ts, auto... Vs>`
- `sizeof...`
- *`...*[]`
- *fold expressions*

### 25.1. Могут ли деструкторы вызывать исключения? Что произойдёт при выполнении данного кода?

```cpp
struct A {
    ~A() noexcept(false) {
        std::cout << "~A()" << std::endl;
        throw std::exception();
    }
};

int main() {
    try {
        A a, b, c;
    } catch (...) { exit(0); }
}
```
### 25.2*. Что произойдёт если убрать `try` блок?

```cpp
struct A {
    ~A() noexcept(false) {
        std::cout << "~A()" << std::endl;
        throw std::exception();
    }
};

int main() {
    A a, b, c;
}
```


# Подготовленно М. Калюжным и И. Фоминым

