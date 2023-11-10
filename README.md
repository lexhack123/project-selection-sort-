# project-selection-sort-
#include <iostream>
#include <string>

// Fonction pour effectuer le tri par sélection
void selectionSort(std::string arr[], int n) {
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

int main() {
    int numNames;
    std::cout << "Combien de noms voulez-vous trier ? ";
    std::cin >> numNames;

    std::string *names = new std::string[numNames];

    std::cout << "Veuillez entrer les noms un par un : " << std::endl;
    for (int i = 0; i < numNames; i++) {
        std::cout << "Nom " << (i + 1) << ": ";
        std::cin >> names[i];
    }

    selectionSort(names, numNames);

    std::cout << "Noms triés : " << std::endl;
    for (int i = 0; i < numNames; i++) {
        std::cout << names[i] << std::endl;
    }

    delete[] names; // N'oubliez pas de libérer la mémoire allouée dynamiquement.

    return 0;
}

