#include <iostream>
#include <fstream>
#include <string>

struct Menu {
    std::string fullName;
    std::string group;
    double price;
};

void addMenuToFile(const Menu& menu) {
    std::ofstream outFile("menu.txt", std::ios::app);
    if (outFile.is_open()) {
        outFile << menu.fullName << "," << menu.group << "," << menu.price << std::endl;
        outFile.close();
        std::cout << "Блюдо успешно добавлено." << std::endl;
    } else {
        std::cerr << "Не удалось открыть файл для записи." << std::endl;
    }
}

void searchMenuByName(const std::string& name) {
    std::ifstream inFile("menu.txt");
    if (inFile.is_open()) {
        std::string line;
        bool found = false;
        while (std::getline(inFile, line)) {
            size_t pos = line.find(',');
            std::string fullName = line.substr(0, pos);
            if (fullName == name) {
                std::cout << "Найдено блюдо: " << line << std::endl;
                found = true;
                break;
            }
        }
        inFile.close();
        if (!found) {
            std::cout << "Блюдо с таким названием не найдено." << std::endl;
        }
    } else {
        std::cerr << "Не удалось открыть файл для чтения." << std::endl;
    }
}

void sortMenuByPrice() {
    std::ifstream inFile("menu.txt");
    if (inFile.is_open()) {
        // Чтение данных и сортировка (пузырьковая сортировка)
        std::string lines[100]; // Предполагаем, что не более 100 блюд
        int count = 0;
        std::string line;
        while (std::getline(inFile, line)) {
            lines[count] = line;
            count++;
        }
        inFile.close();
        for (int i = 0; i < count - 1; i++) {
            for (int j = 0; j < count - i - 1; j++) {
                size_t pos1 = lines[j].find_last_of(',');
                size_t pos2 = lines[j + 1].find_last_of(',');
                double price1 = std::stod(lines[j].substr(pos1 + 1));
                double price2 = std::stod(lines[j + 1].substr(pos2 + 1));
                if (price1 < price2) {
                    std::swap(lines[j], lines[j + 1]);
                }
            }
        }
        // Запись отсортированных данных обратно в файл
        std::ofstream outFile("menu.txt");
        if (outFile.is_open()) {
            for (int i = 0; i < count; i++) {
                outFile << lines[i] << std::endl;
            }
            outFile.close();
            std::cout << "Блюда отсортированы по цене." << std::endl;
        } else {
            std::cerr << "Не удалось открыть файл для записи." << std::endl;
        }
    } else {
        std::cerr << "Не удалось открыть файл для чтения." << std::endl;
    }
}

int main() {
    int choice;
    std::string name;

    do {
        std::cout << "Меню:" << std::endl;
        std::cout << "1. Добавить блюдо" << std::endl;
        std::cout << "2. Поиск блюда по названию" << std::endl;
        std::cout << "3. Сортировать блюда по цене" << std::endl;
        std::cout << "0. Выйти" << std::endl;
        std::cout << "Выберите действие: ";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::cin.ignore();
                std::string fullName, group;
                double price;
                std::cout << "Введите название блюда: ";
                std::getline(std::cin, fullName);
                if (fullName.empty()) {
                    std::cout << "Ввод прерван." << std::endl;
                    break;
                }
                std::cout << "Введите тип блюда: ";
                std::getline(std::cin, group);
                std::cout << "Введите цену блюда: ";
                std::cin >> price;
                Menu newMenu = {fullName, group, price};
                addMenuToFile(newMenu);
                break;
            }
            case 2: {
                std::cin.ignore();
                std::cout << "Введите название блюда: ";
                std::getline(std::cin, name);
                searchMenuByName(name);
                break;
            }
            case 3: {
                sortMenuByPrice();
                break;
            }
            case 0: {
                std::cout << "Программа завершена." << std::endl;
                break;
            }
            default: {
                std::cout << "Неверный выбор. Попробуйте снова." << std::endl;
                break;
            }
        }
    } while (choice != 0);

    return 0;
}
