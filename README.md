#include <iostream>
#include <cmath>
using namespace std;
// Р¤СѓРЅРєС†РёСЏ РІРІРѕРґР° РјР°С‚СЂРёС†С‹
void Input_Matrix(int Lines, int Columns, int Matrix[20][20]) 
{
	for (int i = 0; i < Lines; i++)
	{
		for (int j = 0; j < Columns; j++)
		{
			cout << "Matrix[" << i << "][" << j << "]"; cin >> Matrix[i][j]; 
		}
	}
}
// Р¤СѓРЅРєС†РёСЏ РІС‹РІРѕРґР° РјР°С‚СЂРёС†С‹
void Output_Matrix(int Lines, int Columns, int Matrix[20][20]) 
{
	for (int i = 0; i < Lines; i++)
	{
		for (int j = 0; j < Columns; j++)
		{
			cout.width(7); cout << Matrix[i][j];
		}
	cout << endl;
	}
}
// Р¤СѓРЅРєС†РёСЏ РїРµСЂРµРјРЅРѕР¶РµРЅРёСЏ РґРІСѓС… РјР°С‚СЂРёС†
void Mult_Matrix(int Lines1, int Lines2, int Columns1, int Columns2, int Matrix1[20][20], int Matrix2[20][20], int Fin_Matrix[20][20])
{
	int Lines3 = Lines1;
	int Columns3 = Columns2; 
	for (int i = 0; i < Lines3; i++)
	{
		for (int j = 0; j < Columns3; j++)
		{
			Fin_Matrix[i][j] = 0;
			for (int k = 0; k < Columns3; k++)
			{
				Fin_Matrix[i][j] += Matrix1[i][k] * Matrix2[k][j];
			}
		}
	}
	Output_Matrix(Lines3, Columns3, Fin_Matrix);
}
// Р¤СѓРЅРєС†РёСЏ РѕСЃРІРѕР±РѕР¶РґРµРЅРёСЏ РїР°РјСЏС‚Рё, РІС‹РґРµР»РµРЅРЅРѕР№ РїРѕРґ РґРІСѓРјРµСЂРЅС‹Р№ РґРёРЅР°РјРёС‡РµСЃРєРёР№ РјР°СЃСЃРёРІ
void Clear_Memory(int** Matrix, int Size) 
{ 
    for (int i = 0; i < Size; i++) 
	{
        delete[] Matrix[i];
    }
        delete [] Matrix;        
}
// Р РµРєСѓСЂСЃРёРІРЅР°СЏ С„СѓРЅРєС†РёСЏ РІС‹С‡РёСЃР»РµРЅРёСЏ РѕРїСЂРµРґРµР»РёС‚РµР»СЏ РјР°С‚СЂРёС†С‹
int Find_Det(int** Matrix, int Size) 
{ 
    if (Size == 1)
        return Matrix[0][0];
    else if (Size == 2)
        return Matrix[0][0] * Matrix[1][1] - Matrix[0][1] * Matrix[1][0];
    else 
	{
        int Det = 0;
        for (int k = 0; k < Size; k++) 
		{
            int** M = new int*[Size-1];
                for (int i = 0; i < Size - 1; i++) 
				{
                    M[i] = new int[Size - 1];
            	}
            for (int i = 1; i < Size; i++) 
			{
                int t = 0;
                for (int j = 0; j < Size; j++) 
				{
                    if (j == k)
                        continue;
                    M[i-1][t] = Matrix[i][j];
                    t++;
                }
            }
            Det += pow(-1, k + 2) * Matrix[0][k] * Find_Det(M, Size - 1);
            Clear_Memory(M, Size - 1);
        }
        return Det;
    }
}
 
int main() 
{
	int Variant;
	cout << "1. Quadratic equation" << endl;
	cout << "2. Deteminant of square matrix" << endl;
	cout << "3. Multiplication matrix on matrix" << endl;
	cout << "4. Transposition of matrix" << endl;
	cout << "5. Multiplication matrix on number" << endl;
	cout << "0. Exit" << endl;
	cout << "Choose variant: ";
	cin >> Variant;
	switch(Variant)
	{
		case 1:
		{
			system("cls");
			float First_coeff;
			float Second_coeff;
			float Third_coeff;
			float x_0, x_1, x_2;
			float D;
			cout << "Input coefficiens of equetion" << endl;
			// Р’РІРѕРґ РїРµСЂРІРѕРіРѕ РєРѕСЌС„С„РёС†РёРµРЅС‚Р°, РІС‚РѕСЂРѕРіРѕ РєРѕСЌС„С„РёС†РёРµРЅС‚Р°, С‚СЂРµС‚СЊРµРіРѕ РєРѕСЌС„С„РёС†РёРµРЅС‚Р°
			cout << "First coefficient: "; cin >> First_coeff;
			cout << "Second coefficient: "; cin >> Second_coeff;
			cout << "Third coefficient: "; cin >> Third_coeff; 
			// Р’С‹С‡РёСЃР»РµРЅРёРµ РґРёСЃРєСЂРёРјРёРЅР°РЅС‚Р°
			D = Second_coeff * Second_coeff - 4 * First_coeff * Third_coeff; 
			cout << "\n";
			cout << "D = " << D << endl;
			// РџСЂРѕРІРµСЂРєР° РЅР° РЅР°Р»РёС‡РёРµ РєРѕСЂРЅРµР№ СѓСЂР°РІРЅРµРЅРёСЏ
			if (D < 0) 
			{
				cout << "The discriminant is less than zero. The quadratic equation has no roots" << endl;
			}
			else if (D == 0) 
			{
				x_0 = (-First_coeff) / 2 * First_coeff; //РІС‹С‡РёСЃР»РµРЅРёРµ РµРґРёРЅСЃС‚РІРµРЅРЅРѕРіРѕ РєРѕСЂРЅСЏ СѓСЂР°РІРЅРµРЅРёСЏ
				cout << "The discriminant is zero. The quadratic equation has 1 real root"<< " " << "x = " << x_0 << endl;
			}
			else if (D > 0) 
			{
				x_1 = (-Second_coeff + sqrt(D)) / (2 * First_coeff); //РІС‹С‡РёСЃР»РµРЅРёРµ 1-РіРѕ РєРѕСЂРЅСЏ СѓСЂР°РІРЅРµРЅРёСЏ
				x_2 = (-Second_coeff - sqrt(D)) / (2 * First_coeff); //РІС‹С‡РёСЃР»РµРЅРёРµ 2-РіРѕ РєРѕСЂРЅСЏ СѓСЂР°РІРЅРµРЅРёСЏ
				cout << "The discriminant is greater than zero. The quadratic equation has 2 real roots:" << endl;
				cout << "x_1 = " << x_1 << endl;
				cout << "x_2 = " << x_2 << endl;	
			}
			break;
		}
		case 2:
		{
			system("cls");
		    int Size;
		    cout << "Input a size of matrix: "; cin >> Size; // Р’РІРѕРґ СЂР°Р·РјРµСЂР° РєРІР°РґСЂР°С‚РЅРѕР№ РјР°С‚СЂРёС†С‹
		    int** Matrix = new int*[Size]; //РћР±СЉСЏРІР»СЏРµРј РјР°С‚СЂРёС†Сѓ
		    for (int i = 0; i < Size; i++) 
			{
		        Matrix[i] = new int[Size];
		    }
		    cout << "\n";
			cout << "Input a matrix: " << endl; // Р’РІРѕРґ СЌР»РµРјРµРЅС‚РѕРІ РјР°С‚СЂРёС†С‹
		    for (int Lines = 0; Lines < Size; Lines++) 
			{
		        for (int Columns = 0; Columns < Size; Columns++) 
				{
		        	cout << "Matrix[" << Lines << "][" << Columns << "]";
		            cin >> Matrix[Lines][Columns]; 
		        }
		    }
		    cout << "\n";
			cout << "Found determinant: " << Find_Det(Matrix, Size) << endl; // Р’С‹РІРѕРґ РѕРїСЂРµРґРµР»РёС‚РµР»СЏ РјР°С‚СЂРёС†С‹
		    Clear_Memory(Matrix, Size);
		    break;
		}
		case 3:
		{
			system("cls");
			int Matrix1[20][20], Matrix2[20][20];
			int Lines1, Lines2, Lines3;
			int Columns1, Columns2, Columns3;
			int Fin_Matrix[20][20];
			cout << "Lines and columns of first matrix" << endl; // Р’РІРѕРґ СЂР°Р·РјРµСЂР° РїРµСЂРІРѕР№ РјР°С‚СЂРёС†С‹ 
			cout << "Lines: "; cin >> Lines1;
			cout << "Columns: "; cin >> Columns1; 
			cout << "\n";
			cout << "Input first matrix" << endl; // Р’РІРѕРґ СЌР»РµРјРµРЅРѕРІ РїРµСЂРІРѕР№ РјР°С‚СЂРёС†С‹
			Input_Matrix(Lines1, Columns1, Matrix1);
			cout << "\n";
			cout << "First matrix: "<< endl; // Р’С‹РІРѕРґ РїРµСЂРІРѕР№ РјР°С‚СЂРёС†С‹
			Output_Matrix(Lines1, Columns1, Matrix1);
			cout << "\n";
			cout << "Lines and columns of second matrix" << endl; // Р’РІРѕРґ РІС‚РѕСЂРѕ РјР°С‚СЂРёС†С‹
			cout << "Lines: "; cin >> Lines2;
			cout << "Columns: "; cin >> Columns2;
			cout << "\n";
			cout << "Input second matrix" << endl; // Р’РІРѕРґ СЌР»РµРјРµС‚РѕРІ РІС‚РѕСЂРѕР№ РјР°С‚СЂРёС†С‹
			Input_Matrix(Lines2, Columns2, Matrix2);
			cout << "\n";
			cout << "Second matrix: " << endl; // Р’С‹РІРѕРґ РІС‚РѕСЂРѕР№ РјР°С‚СЂРёС†С‹
			Output_Matrix(Lines2, Columns2, Matrix2);
			system("pause"); 
			system("cls"); 
			cout << "First matrix: "<< endl; // РџРѕРІС‚РѕСЂРЅС‹Р№ РІС‹РІРѕРґ РїРµСЂРІРѕР№ РјР°С‚СЂРёС†С‹
			Output_Matrix(Lines1, Columns1, Matrix1);
			cout << "\n";
			cout << "Second matrix: " << endl; // РџРѕРІС‚РѕСЂРЅС‹Р№ РІС‹РІРѕРґ РІС‚РѕСЂРѕР№ РјР°С‚СЂРёС†С‹
			Output_Matrix(Lines2, Columns2, Matrix2);
			Lines3 = Lines1;
			Columns3 = Columns2;
			cout << "\n";
			if (Columns1 != Lines2) // РџСЂРѕРІРµСЂРєР° РЅР° РІРѕР·РјРѕР¶РЅРѕСЃС‚СЊ РїРµСЂРµРјРЅРѕР¶РµРЅРёСЏ
			{
				cout << "Unreal";
			}
			else
			{
				cout << "Composition:" << endl; // РџСЂРѕРёР·РІРµРґРµРЅРёРµ РјР°С‚СЂРёС†
				Mult_Matrix(Lines1, Lines2, Columns1, Columns2, Matrix1, Matrix2, Fin_Matrix);
			}
			break;
		}
		case 4:
		{
			system("cls");
			int Lines, Columns;
			int Matrix[20][20];
			// Р’РІРѕРґ С‡РёСЃР»Р° СЃС‚СЂРѕРє Рё СЃС‚РѕР»Р±С†РѕРІ РјР°С‚СЂРёС†С‹
			cout << "Input number of lines: "; cin >> Lines;
			cout << "Input number of columns: "; cin >> Columns;
			Input_Matrix(Lines, Columns, Matrix);
			cout << "\n";
			cout << "Source matrix:" << endl; // Р’С‹РІРѕРґ РёСЃС…РѕРґРЅРѕР№ РјР°С‚СЂРёС†С‹
			Output_Matrix(Lines, Columns, Matrix);
			cout << "\n";
			cout << "Transposed matrix:" << endl; // Р’С‹РІРѕРґ С‚СЂР°РЅСЃРїРѕРЅРёСЂРѕРІР°РЅРЅРѕР№ РјР°С‚СЂРёС†С‹
			for (int j = 0; j < Columns; j++)
			{
				for (int i = 0; i < Lines; i++)
				{
					for (int k = 0; k < Columns; k++)
					{
						if (k == j)
						{
							Matrix[j][i] = Matrix[i][k];
							cout.width(7); cout << Matrix[j][i];
						}
					}
				}
				cout << endl;
			}
			break;
		}
		case 5:
		{
			system("cls");
			int Lines, Columns, Multiplier;
			int Matrix[20][20];
			// Р’РІРѕРґ РєРѕР»РёС‡РµСЃС‚РІР° СЃС‚СЂРѕРє Рё СЃС‚РѕР»Р±С†РѕРІ РјР°С‚СЂРёС†С‹
			cout << "Input number of lines: "; cin >> Lines;
			cout << "Input number of columns: "; cin >> Columns;
			Input_Matrix(Lines, Columns, Matrix);
			cout << "\n";
			cout << "Input multiplier: "; cin >> Multiplier;
			for (int i = 0; i < Lines; i++)
			for (int j = 0; j < Columns; j++)
			{
				Matrix[i][j] *= Multiplier; // РЈРјРЅРѕР¶РµРЅРёРµ РєР°Р¶РґРѕРіРѕ СЌР»РµРјРµРЅС‚Р° РЅР° С‡РёСЃР»Рѕ
			}
			cout << "\n";
			cout << "Composed matrix:" << endl;
			Output_Matrix(Lines, Columns, Matrix); // Р’С‹РІРѕРґ РїСЂРѕРёР·РІРµРґРµРЅРёСЏ РјР°С‚СЂРёС†С‹ Рё С‡РёСЃР»Р°
			break;
		}
		case 0:
		{
			system("cls");
			cout << "Bye :)" << endl;
			break;
		}
	}
}
