#include <iostream>
#include <fstream>
#include <string>
#include <windows.h>

// Функция для сортировки выбором
void selectionSort(std::string arr[], int n) {
    // Применение сортировки выбором
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        if (minIndex != i) {
            std::swap(arr[i], arr[minIndex]);
        }
    }
}

void saveNamesToFile(const std::string arr[], int n, const std::string& filename) {
    // Открытие файла для записи
    std::ofstream file(filename);
    if (file.is_open()) {
        // Запись имен в файл
        for (int i = 0; i < n; i++) {
            file << arr[i] << std::endl;
        }
        // Закрытие файла
        file.close();
        std::cout << "Имена сохранены в файле '" << filename << "'." << std::endl;
    }
    else {
        // В случае ошибки открытия файла
        std::cerr << "Ошибка открытия файла для сохранения." << std::endl;
    }
}


int main() {
    // Установка кодировки для консоли (1251 - русская кодировка)
    SetConsoleCP(1251);
    SetConsoleOutputCP(1251);

    int numNames;
    // Запрос у пользователя количества имен для сортировки
    std::cout << "Сколько имен вы хотите отсортировать? ";
    std::cin >> numNames;

    // Выделение памяти под массив имен
    std::string* names = new std::string[numNames];

    // Ввод имен от пользователя
    std::cout << "Введите имена одно за другим: " << std::endl;
    for (int i = 0; i < numNames; i++) {
        std::cout << "Имя " << (i + 1) << ": ";
        std::cin >> names[i];
    }

    int choice;
    // Основной цикл программы
    do {
        // Вывод меню
        std::cout << "\nМеню:\n";
        std::cout << "1. Вывести отсортированные имена\n";
        std::cout << "2. Сохранить в файл\n";"
        std::cout << "Выберите действие: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                // Сортировка и вывод отсортированных имен
                selectionSort(names, numNames);
                std::cout << "Отсортированные имена: " << std::endl;
                for (int i = 0; i < numNames; i++) {
                    std::cout << names[i] << std::endl;
                }
                break;
           case 2:
            // Сохранение имен в файл
            saveNamesToFile(names, numNames, "sorted_names.txt");
            std::cout << "Имена сохранены в файле 'sorted_names.txt'." << std::endl;
            case 3:
                std::cout << "Выход из программы." << std::endl;
                break;
            default:
                std::cout << "Некорректный выбор. Пожалуйста, выберите снова." << std::endl;
        }

    } while (choice != 3);

    // Освобождение выделенной памяти
    delete[] names;

    return 0;
}
}

