#include <iostream>
#include <vector>
#include <cmath>


using namespace std;

void gaussianElimination(vector<vector<double>> &A, vector<double> &B, vector<double> &solution, int n) {
    for (int i = 0; i < n; ++i) {
        // Pivot: find the row with the largest element in the current column
        int maxRow = i;
        for (int k = i + 1; k < n; ++k) {
            if (abs(A[k][i]) > abs(A[maxRow][i])) {
                maxRow = k;
            }
        }

        // Swap the max row with the current row
        swap(A[i], A[maxRow]);
        swap(B[i], B[maxRow]);

        // Eliminate the below rows
        for (int k = i + 1; k < n; ++k) {
            double factor = A[k][i] / A[i][i];
            for (int j = i; j < n; ++j) {
                A[k][j] -= factor * A[i][j];
            }
            B[k] -= factor * B[i];
        }
    }

    // Back substitution
    solution.assign(n, 0);
    for (int i = n - 1; i >= 0; --i) {
        solution[i] = B[i] / A[i][i];
        for (int j = i - 1; j >= 0; --j) {
            B[j] -= A[j][i] * solution[i];
        }
    }
}

int main() {
    int n;

    cout << "Enter the number of (x, f(x)) pairs: ";
    cin >> n;

    if (n < 2) {
        cout << "You need at least 2 points to define a polynomial!" << endl;
        return -1;
    }

    vector<vector<double>> A(n, vector<double>(n));
    vector<double> B(n), solution(n);
    vector<pair<double, double>> points(n);

    cout << "Enter the pairs of (x, f(x)) values:" << endl;
    for (int i = 0; i < n; ++i) {
        cout << "Enter x" << i + 1 << " and f(x" << i + 1 << "): ";
        cin >> points[i].first >> points[i].second;
    }

    for (int i = 0; i < n; ++i) {
        double x = points[i].first;
        for (int j = 0; j < n; ++j) {
            A[i][j] = pow(x, n - j - 1);
        }
        B[i] = points[i].second;
    }

    gaussianElimination(A, B, solution, n);

    cout << "The polynomial is: f(x) = ";
    for (int i = 0; i < n; ++i) {
        if (i != 0 && solution[i] >= 0) cout << "+ ";
        cout << solution[i];
        if (n - i - 1 > 0) cout << "x^" << (n - i - 1) << " ";
    }
    cout << endl;

    cout << "The constant term (c) is: " << solution[n-1] << endl;

    return 0;
}
