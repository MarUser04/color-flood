#include <iostream>
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>
#include <windows.h>

struct tablero{
	int **matriz;
	int filas, columnas;
	char boton;
	int aux2;
	int cont;
};

void cargarmatriz(tablero *tmc);
void imprimir(tablero *tmc);
void color(int X);
void gotoxy(int x,int y);
void menu();
void seleccion(tablero *tmc);


int main(int argc, char** argv) {
	srand(time(0));
	system("color f0");
	
	tablero tm;

	char tecla, esc;
	int band=0, band1=0;
	
	menu();
	
	do{	
	
		tecla=getch( );
		switch(tecla){
			case 49:{
				
				system("cls");
				band=1;
				break;
			}
			case 50:{
	          
	          system("cls");
	         
	          do{
	          	printf("\n\nSI DESEA REGRESAR AL MENU PRINCIPAL PRESIONE (4).");
	        	 esc=getch();
	            
	             if(esc!='4'){
	          	     printf("\n OPCION INVALIDA, INTENTE DE NUEVO");
				  }
	          	
	          	
			  }while(esc!='4');
	          
	          if(esc=='4'){
	          	
	          	band1=1;
	          	system("cls");
			  }
				
				break;
			}
			case 51:{
				system("cls");
				printf("CREADOR: MARCO JOSE USECHE RIVERA\n ESTUDIANTE INGENIERIA EN INFORMATICA\n UNET 2016 ");
				do{
	          	  printf("\n\nSI DESEA REGRESAR AL MENU PRINCIPAL PRESIONE (4).");
	            	esc=getch();
	          	  if(esc!= '4'){
	          	     printf("\n OPCION INVALIDA, INTENTE DE NUEVO");
				  }
				  
	          	
			   }while(esc!='4');
	          
	           if(esc=='4'){
	          	
	          	band1=1;
	          	system("cls");
			   }
				break;
			}
			default:{
			
				
				gotoxy(26,8);
				printf("\n OPCION INVALIDA, INTENTE DE NUEVO");
				
				break;
			}
			
		}//switch
		
		 if(band1==1){
	    	
	       menu( );
	   
	     }
		
		
	}while(band!=1);
	
	if(band==1){
		system("cls");
			tablero tmc;
        	cargarmatriz(&tmc);
	
	}
	

	system("pause>null");
	return 0;
}

void color(int X) 
{ 
SetConsoleTextAttribute(GetStdHandle (STD_OUTPUT_HANDLE),X); 
} 

void gotoxy(int x,int y){  
      HANDLE hcon;  
      hcon = GetStdHandle(STD_OUTPUT_HANDLE);  
      COORD dwPos;  
      dwPos.X = x;  
      dwPos.Y= y;  
      SetConsoleCursorPosition(hcon,dwPos);  
 } 
 
void cargarmatriz(tablero *tmc)
{
	char opc; 
	int aux;
	do{
	system("cls");
	printf("-------SELECCIONE SU DIFICULTAD-------\n");
	printf("-1-----FACIL-----\n");
	printf("-2-----MEDIO-----\n");
	printf("-3-----DIFICIL---\n");

    
    fflush(stdin);
    opc= getch();
    
    aux=opc-48;
	}while(aux<1 || aux>4);
	
	switch(aux)
	{
		case 1:
			tmc->filas=10;
			tmc->columnas=10;
			break;
		case 2:
			tmc->filas=15;
			tmc->columnas=15;
			break;
		case 3:
			tmc->filas=20;
			tmc->columnas=20;
			break;
	
	}
	
	if(tmc->filas==10)
	{
		tmc->cont= 18;
	}
	else if(tmc->filas==15)
	{
		tmc->cont= 27;
	}
	else if(tmc->filas==20)
	{
		tmc->cont=36;
	}
	

	tmc->matriz= new int *[tmc->filas];
	for(int i=0; i<tmc->filas; i++)
	{
		tmc->matriz[i]=new int [tmc->columnas];
	}
	


	
	
	for(int i=0;i<tmc->filas;i++){
		for(int j=0;j<tmc->columnas;j++){
			tmc->matriz[i][j]=rand()%6+1;
		}
	}
	
	imprimir(tmc);
	
	seleccion(tmc);

	/////////////////////
	
	
	
	tmc->matriz[0][0]=9;
	
	do
	{
		

	do{
		
	
	fflush(stdin);
	tmc->boton=getch();
	tmc->aux2=tmc->boton-48-48;
	
	}while(!(tmc->aux2==1 || tmc->aux2==2 || tmc->aux2==3 || tmc->aux2==4 || tmc->aux2==5 || tmc->aux2==6));

	tmc->cont--;
	

	
	for(int i=0; i<tmc->filas; i++)
	{
		for(int j=0; j< tmc->columnas; j++)
		{
			if(tmc->matriz[i][j]==9)
			{
				if(tmc->matriz[i+1][j]==tmc->aux2)
				{
					tmc->matriz[i+1][j]=9;
				}
				if(i-1>=0 && tmc->matriz[i-1][j]==tmc->aux2)
				{
					tmc->matriz[i-1][j]=9;
				}
				if(j-1>=0 && tmc->matriz[i][j-1]==tmc->aux2)
				{
					tmc->matriz[i][j-1]=9;
				}
				if( tmc->matriz[i][j+1]==tmc->aux2)
				{
					tmc->matriz[i][j+1]=9;
				}
			}
		}
	}

	
	/*printf("\n\n\n");                           //impresion de matriz con numeros
	for(int i=0; i< tmc->filas-1; i++)
	{
		printf("\n");
		for(int j=0; j< tmc->columnas-1; j++)
		{
			printf("%d", tmc->matriz[i][j]);
		}
	}*/
	
	system("cls");
	imprimir(tmc);
	seleccion(tmc);
	
	
	}while(tmc->cont >0);

}

void imprimir(tablero *tmc)
{
	for(int i=0;i<tmc->filas;i++){
		printf("\n");
		for(int j=0;j<tmc->columnas;j++){
			if(tmc->matriz[i][j]==1)
			{
				color(15*16+9);
				printf("%c", 219);
			}
			else if(tmc->matriz[i][j]==2)
			{
				color(15*16+12);
				printf("%c", 219);
			}
				else if(tmc->matriz[i][j]==3)
			{
				color(15*16+11);
				printf("%c", 219);
			}
				else if(tmc->matriz[i][j]==4)
			{
				color(15*16+14);
				printf("%c", 219);
			}
				else if(tmc->matriz[i][j]==5)
			{
				color(15*16+13);
				printf("%c", 219);
			}
			else if(tmc->matriz[i][j]==6 )
			{
				color(15*16+10);
				printf("%c", 219);
			}
			else if(tmc->matriz[i][j]==9)
			{
				switch(tmc->aux2)
				{
					case 1:
						color(15*16+9);
						printf("%c", 219);
						break;
					case 2:
						color(15*16+12);
						printf("%c", 219);
						break;
					case 3:
						color(15*16+11);
						printf("%c", 219);
						break;
					case 4:
						color(15*16+14);
						printf("%c", 219);
						break;
					case 5:
						color(15*16+13);
						printf("%c", 219);
						break;
					case 6:
						color(15*16+10);
						printf("%c", 219);
						break;
				}
			}
			
		}
	}
	
	
}

void menu()
{
	printf("\t-------BIENVENIDO A COLORFLOOD---USECHE EDITION V. 0.2 CON BUGS---------\n");
	printf("\n\n\t-------(1)MODOS DE JUEGO----\n");
	printf("\t-------(2)AYUDA-------------\n");
	printf("\t-------(3)CREDITOS----------\n");
}

void seleccion(tablero *tmc)
{
	
	gotoxy(25, 3);
	color(15*16+8);
	printf("MOVIMIENTOS: %d", tmc->cont);
	
	
	gotoxy(25, 5);
	color(15*16+9);
	printf("%c%c%c A", 219, 219, 219);
	
	gotoxy(25, 7);
	color(15*16+12);
	printf("%c%c%c B", 219, 219, 219);
	
	gotoxy(25, 9);
	color(15*16+11);
	printf("%c%c%c C", 219, 219, 219);
	
	gotoxy(25, 11);
	color(15*16+14);
	printf("%c%c%c D", 219, 219, 219);
	
	gotoxy(25, 13);
	color(15*16+13);
	printf("%c%c%c E", 219, 219, 219);
	
	gotoxy(25, 15);
	color(15*16+10);
	printf("%c%c%c F", 219, 219, 219);
}
