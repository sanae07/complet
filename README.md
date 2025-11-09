
#include <stdio.h>

// Calcul du PGCD avec l'algorithme d'Euclide
int pgcd(int a, int b) {
    while (b != 0) {
        int r = a % b;
        a = b;
        b = r;
    }
    return a;
}

// Algorithme d'Euclide étendu
// Retourne d et les valeurs x0, y0 telles que : d = a*x0 + b*y0
int euclide_etendu(int a, int b, int *x0, int *y0) {
    if (b == 0) {
        *x0 = 1; 
        *y0 = 0;
        return a;
    }

    int x1, y1;
    int d = euclide_etendu(b, a % b, &x1, &y1);

    *x0 = y1;
    *y0 = x1 - (a / b) * y1;

    return d;
}

int main() {
    int a, b, c;
    printf("Entrez les valeurs de a, b et c (ax + by = c) : ");
    scanf("%d %d %d", &a, &b, &c);

    int x0, y0;
    int d = euclide_etendu(a, b, &x0, &y0);

    // Vérification de l'existence de solutions entières
    if (c % d != 0) {
        printf("\nPas de solution entiere car %d ne divise pas %d.\n", d, c);
        return 0;
    }

    // Calcul d'une solution particulière
    int xp = x0 * (c / d);
    int yp = y0 * (c / d);

    // Coefficients de la solution générale
    int alpha = b / d;
    int beta = -a / d;

    printf("\nIl existe des solutions entieres car %d divise %d.\n", d, c);
    printf("\nSolution particuliere : (x_p, y_p) = (%d, %d)\n", xp, yp);

    printf("\nSolution generale :\n");
    printf("(x, y) = (%d + %d*k , %d + %d*k) , k ∈ Z\n", xp, alpha, yp, beta);

    return 0;
}
