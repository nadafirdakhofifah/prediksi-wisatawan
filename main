#include <iostream>
#include <vector>
#include <iomanip>
#include <cmath>

using namespace std;

double mean(const vector<double>& data) {
    double sum = 0.0;
    for (double val : data) {
        sum += val;
    }
    return sum / data.size();
}

// Fungsi untuk menghitung MAPE
double calculateMAPE(const vector<double>& actual, const vector<double>& predicted) {
    double sumError = 0.0;
    for (size_t i = 0; i < actual.size(); ++i) {
        sumError += abs((actual[i] - predicted[i]) / actual[i]);
    }
    return (sumError / actual.size()) * 100;
}

int main() {

    cout << "\n-------------------------------------------------------------------------";
    cout << "\n  Nama: Intan Putri Mansyur Pratama        Nama: Nada Firda Khofifah\n";
    cout << "\n  NPM: 163                                 NPM: 202\n";
    cout << "-------------------------------------------------------------------------\n";
    cout << "\n=========================================================================";
    cout << "\n          Prediksi Strategis Kunjungan Wisatawan Mancanegara";
    cout << "\n                 ke Indonesia dengan Regresi Linear";
    cout << "\n=========================================================================";

    int n;
    cout << "\nMasukkan jumlah data (bulan): ";
    cin >> n;

    vector<double> X1(n), X2(n), X3(n), Y(n);
    cout << "Masukkan data (X1, X2, X3, Y) untuk setiap bulan:\n";

    for (int i = 0; i < n; ++i) {
        cout << "---------------------------------------------\n";
        cout << "Bulan ke-" << i + 1 << ":\n";
        cout << "  X1 (Wisatawan Pintu Masuk Udara): ";
        cin >> X1[i];
        cout << "  X2 (Wisatawan Pintu Masuk Darat): ";
        cin >> X2[i];
        cout << "  X3 (Wisatawan Pintu Masuk Laut): ";
        cin >> X3[i];
        cout << "  Y (Jumlah Total Wisatawan): ";
        cin >> Y[i];
    }

    double meanX1 = mean(X1);
    double meanX2 = mean(X2);
    double meanX3 = mean(X3);
    double meanY = mean(Y);

    double SXX1 = 0, SXX2 = 0, SXX3 = 0, SXY1 = 0, SXY2 = 0, SXY3 = 0;
    double SXX12 = 0, SXX13 = 0, SXX23 = 0;

    for (int i = 0; i < n; ++i) {
        SXX1 += (X1[i] - meanX1) * (X1[i] - meanX1);
        SXX2 += (X2[i] - meanX2) * (X2[i] - meanX2);
        SXX3 += (X3[i] - meanX3) * (X3[i] - meanX3);
        SXY1 += (X1[i] - meanX1) * (Y[i] - meanY);
        SXY2 += (X2[i] - meanX2) * (Y[i] - meanY);
        SXY3 += (X3[i] - meanX3) * (Y[i] - meanY);
        SXX12 += (X1[i] - meanX1) * (X2[i] - meanX2);
        SXX13 += (X1[i] - meanX1) * (X3[i] - meanX3);
        SXX23 += (X2[i] - meanX2) * (X3[i] - meanX3);
    }

    double denominator = SXX1 * (SXX2 * SXX3 - SXX23 * SXX23) - SXX12 * (SXX12 * SXX3 - SXX13 * SXX23) + SXX13 * (SXX12 * SXX23 - SXX13 * SXX2);

    if (denominator == 0) {
        cout << "Error: Data tidak cukup untuk menghitung regresi." << endl;
        return 1;
    }

    double B1 = (SXY1 * (SXX2 * SXX3 - SXX23 * SXX23) - SXY2 * (SXX12 * SXX3 - SXX13 * SXX23) + SXY3 * (SXX12 * SXX23 - SXX13 * SXX2)) / denominator;
    double B2 = (SXX1 * (SXY2 * SXX3 - SXY3 * SXX23) - SXY1 * (SXX12 * SXX3 - SXX13 * SXX23) + SXX13 * (SXY1 * SXX23 - SXY3 * SXX12)) / denominator;
    double B3 = (SXX1 * (SXX2 * SXY3 - SXX23 * SXY2) - SXX12 * (SXY1 * SXX3 - SXX13 * SXY3) + SXY1 * (SXX12 * SXX23 - SXX13 * SXX2)) / denominator;
    double A = meanY - B1 * meanX1 - B2 * meanX2 - B3 * meanX3;

    cout << fixed << setprecision(4);
    cout << "\nNilai slope (B1): " << B1 << "\n";
    cout << "Nilai slope (B2): " << B2 << "\n";
    cout << "Nilai slope (B3): " << B3 << "\n";
    cout << "Nilai intercept (A): " << A << "\n";
    cout << "Persamaan regresi: Y = " << A << " + " << B1 << " * X1 + " << B2 << " * X2 + " << B3 << " * X3\n";

    double X1_input, X2_input, X3_input;
    cout << "\nMasukkan nilai X1, X2, dan X3 untuk memprediksi Y:\n";
    cout << "  X1 (Wisatawan Pintu Masuk Udara): ";
    cin >> X1_input;
    cout << "  X2 (Wisatawan Pintu Masuk Darat): ";
    cin >> X2_input;
    cout << "  X3 (Wisatawan Pintu Masuk Laut): ";
    cin >> X3_input;

    double Y_prediksi = A + B1 * X1_input + B2 * X2_input + B3 * X3_input;
    cout << "\nPrediksi Y (Jumlah Total Wisatawan): " << Y_prediksi << "\n";

    double Y_aktual;
    cout << "Masukkan nilai aktual untuk bulan selanjutnya: ";
    cin >> Y_aktual;

    double mape = calculateMAPE({Y_aktual}, {Y_prediksi});
    cout << "\nMean Absolute Percentage Error (MAPE): " << mape << "%\n";

    return 0;
}
