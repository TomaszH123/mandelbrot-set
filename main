#include <stdio.h>
#include <stdlib.h>
#include <SDL.h>
#include <math.h>
#include <complex.h>
#include <tgmath.h>
#include <windows.h>

int check_number(_Dcomplex imag);
int convert_coords(int value);
int convert_coords_x(double x);
int convert_coords_y(double y);


int main() {
	SDL_Init(SDL_INIT_VIDEO);
	SDL_Window* window = SDL_CreateWindow("abcd", 500, 100, 800, 800, SDL_WINDOW_SHOWN);
	SDL_Renderer* renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC);
	int running = 1;
	SDL_Event event;




	SDL_SetRenderDrawColor(renderer, 0, 0, 255, 255);
	while (running) {
		while (SDL_PollEvent(&event)) {
			if (event.type == SDL_QUIT) {
				running = 0;
			}
		}
		
		
		double a = -2;
		double b = 2;
		_Dcomplex z = { a, b };
		for (int i = 0; i < 800; i++) {
			for (int j = 0; j < 800; j++) {
				if (check_number(z)) {
					SDL_RenderDrawPoint(renderer, convert_coords_x(a), convert_coords_y(b));
					//printf("%d  %d\n", convert_coords_x(a), convert_coords_y(b));
					//SDL_RenderPresent(renderer);
				}
				a = a + 0.005;
				z._Val[0] = a;
				z._Val[1] = b;
			}
			b = b - 0.005;
			a = -2; // Reset 'a' for the next row
			z._Val[0] = a;
			z._Val[1] = b;
		}

		//_Dcomplex z = { 1, 0 };
		//printf("%d\n", check_number(z));

		SDL_RenderPresent(renderer);
	}

	return 0;
}

int check_number(_Dcomplex imag) {	// returns 1 if a number is inside the set
	_Dcomplex z = { 0, 0 };
	//_Dcomplex a = { 0, 0 };

	for (int n = 0; n < 200; n++) {
		_Dcomplex a = _Cmulcc(z, z);
		z = _Cbuild(creal(a) + creal(imag), cimag(a) + cimag(imag));
		//printf("z: %f + %fi, n:%d\n", creal(z), cimag(z), n);

		if (sqrt(creal(z) * creal(z) + cimag(z) * cimag(z)) > 2) {
			return 0;
		}
	}
	return 1;
}

int convert_coords(int value) {
	double x_range = 2.0;
	double x_center = (double)800 / 2.0;
	double x_scale = (double)800 / x_range;

	int x_screen = (int)(value * x_scale + x_center);
	return x_screen;
}

int convert_coords_x(double x) {
	int a = (x + 2) * 200;
	return a;
}

int convert_coords_y(double y) {
	int a = 800 - ((y + 2) * 200);
	return a;
}
