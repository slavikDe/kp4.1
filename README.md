# kp4.1#include <stdio.h>   
#include <math.h>
#include <conio.h>
#include <locale.h>



float my_cos(float angle, float e) {
	double result = 1;
	double delta = 1;

	for (int i = 0;; i++) {
		delta *= -(angle * angle) / ((i * 2 + 2) * (i * 2 + 1));
		if (fabs(delta) <= e) 
			break;
		result += delta;
	}
	return result;
}

int main()
{
	
	setlocale(LC_ALL, "");
	float e, x1, x2, krok, pi = 3.14159265358979323846;
	printf("Для обчислення значень cos вам потрiбно ввести межi обчислення (перше та останнє значення), точнiть i крок.\n");

	printf("Введiть початкове значення косинуса : ");
	if (!scanf_s("%f", &x1) ) { printf("Початкове значення косинуса повинне бути числом!"); return 0; }

	printf("Введiть останнє значення косинуса: ");
	if (!scanf_s("%f", &x2)  ) { printf("Останнє значення косинуса повинне бути числом!"); return 0;}

	printf("Введіть крок :");
	if (!scanf_s("%f", &krok) || krok == 0) { printf("Крок не може дорівнювати 0."); return 0; }

	printf("Введіть точність (0.0001 - 4 значення після коми) : ");
	if (!scanf_s("%f", &e) || e <= 0) { printf("Точність повнна бути числом у вигляді 0.001."); return 0; }

	if (x1 < x2) { krok = krok; }
	else   { krok = -krok; }

	printf("\t---x---\t\t---cos(x)---\t---sin(Taylor)---\t---sin(x)-sin(Taylor)---\n");
	
	float x = x1;
	while (x < x2) {
		float cosx = cos(x * pi / 180) ;
		float costey = my_cos(x * pi / 180, e);
		printf("\t%f\t%f\t%f\t\t%f\n", x, cosx, costey, cosx - costey);

		x += krok;
	}
	_getch();
	_getch();
	
	//system("pause");
	return 0;
}
