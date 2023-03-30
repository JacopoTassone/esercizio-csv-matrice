//esercizio-csv-matrice

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define DIM 10

int caricaMatrice();
FILE* apriFile();
void scriviFile();

int main(void) {
  int mat[DIM][DIM];
  FILE *fp;
  int scelta, dim;

  srand(time(NULL));

  do{
    printf("\nInserire la propria scelta:\t");
    scanf("%d", &scelta);
    if(scelta==1){ 
        dim = caricaMatrice(mat);
    }
    if(scelta==2){
        apriFile(fp);
        scriviFile(fp, mat, dim);
    }
  }while(scelta!=0);
  
  
}
int caricaMatrice(int mat[][DIM]){
  int dim;

  do{
    printf("Inserire la dimensione:\t");
    scanf("%d", &dim);
  }while(dim<0 || dim>DIM);

  for(int i=0; i<dim; i++){
    for(int j=0; j<dim; j++){
      mat[i][j] = (rand()%30)+1;
    }
  }

  return dim;
}

FILE* apriFile(FILE* fp){
 fp = fopen("matrice.csv", "w");

  if(fp==NULL){
    printf("\nErrore: apertura file non riuscita\n");
  return 0;
  }

  return fp;
}

void scriviFile(FILE* fp, int mat[][DIM], int dim){
  for(int i=0; i<dim; i++){
    fprintf(fp, "\n");
    for(int j=0; j<dim; j++){
      if(j==dim-1){
        fprintf(fp, "%d", mat[i][j]);
      }else{
        fprintf(fp, "%d, ", mat[i][j]);
      }
    }
  }
}
