#Hilos 
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

typedef struct {
  char word[101];
  int frequency;
} WordArray ;

int compareWords(const void *f1, const void *f2){
  WordArray *a = (WordArray *)f1;
  WordArray *b = (WordArray *)f2;
  return (b->frequency - a->frequency);
}

void countFrequency(void *arg){
  
  char *fileName = (char*)malloc(sizeof(char));
  fileName = (char*)arg;
  WordArray *words = (WordArray*)calloc((1000),sizeof(WordArray));
  char *result = (char*)malloc(sizeof(result)*100);
  int counter = 0;
  int isUnique;
  int i = 0;
  FILE *file;
  char buff[1000];

  // Clear the array, so threads don't modify the program after they've been created
  for (i = 0; i < sizeof(WordArray); i++){
    words[i].word[0] = '\0';
    words[i].frequency = 0;
  }
  
  #Archivo.txt
  no
dos dos
tres tres tres
cuatro cuatro cuatro cuatro
cinco cinco cinco cinco cinco
seis seis seis seis seis seis
siete siete siete siete siete siete siete
ocho ocho ocho ocho ocho ocho ocho ocho
nueve nueve nueve nueve nueve nueve nueve nueve nueve
dies dies dies dies dies dies dies dies dies dies dies
  
  
  
  
  
  #
  #CLIENTE_LINUX
  
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<unistd.h>
#include<arpa/inet.h>
#include<sys/socket.h>
#include<netinet/in.h>
#include<netdb.h>
int main(int argc, char **argv){
  if(argc<2)
  {
    printf("<host> <puerto>\n");
    return 1;
  }
  struct sockaddr_in cliente; //Declaración de la estructura con información para la conexión
  struct hostent *servidor; //Declaración de la estructura con información del host
  servidor = gethostbyname(argv[1]); //Asignacion
  if(servidor == NULL)
  { //Comprobación
    printf("Host erróneo\n");
    return 1;
  }
  int puerto, conexion;
  char buffer[100];
  conexion = socket(AF_INET, SOCK_STREAM, 0); //Asignación del socket
  puerto=(atoi(argv[2])); //conversion del argumento
  bzero((char *)&cliente, sizeof((char *)&cliente)); //Rellena toda la estructura de 0's
        //La función bzero() es como memset() pero inicializando a 0 todas la variables
  cliente.sin_family = AF_INET; //asignacion del protocolo
  cliente.sin_port = htons(puerto); //asignacion del puerto
  bcopy((char *)servidor->h_addr, (char *)&cliente.sin_addr.s_addr, sizeof(servidor->h_length));
  //bcopy(); copia los datos del primer elemendo en el segundo con el tamaño máximo 
  //del tercer argumento.


  //cliente.sin_addr = *((struct in_addr *)servidor->h_addr); //<--para empezar prefiero que se usen
  //inet_aton(argv[1],&cliente.sin_addr); //<--alguna de estas dos funciones
  if(connect(conexion,(struct sockaddr *)&cliente, sizeof(cliente)) < 0)
  { //conectando con el host
    printf("Error conectando con el host\n");
    close(conexion);
    return 1;
  }
  printf("Conectado con %s:%d\n",inet_ntoa(cliente.sin_addr),htons(cliente.sin_port));
  //inet_ntoa(); está definida en <arpa/inet.h>
  printf("Escribe un mensaje: ");
  fgets(buffer, 100, stdin);
  send(conexion, buffer, 100, 0); //envio
  bzero(buffer, 100);
  recv(conexion, buffer, 100, 0); //recepción
  printf("%s", buffer);
return 0;
}

  
  

  file = fopen(fileName, "r");
  if (file == NULL){
    printf("Couldn't open file: ");
  }
      
  else {
    while ( (fscanf(file, "%s", buff)) != EOF)
    {
      isUnique = -1;

      // String comparison - to check if the word is already in the array
      int k;
      for (k = 0; k < counter; k++){
        if (strcmp(words[k].word, buff) == 0){
          isUnique = k;
        }
      }
      // If the string is not in the array, put it in the array
      if (isUnique == -1){
        strcpy(words[counter].word, buff);
        words[counter].frequency = 1;
        counter++;
      }
      // Increase frequency of non-unique words
      else {
        words[isUnique].frequency++;
      }
      // Re-allocate memory for the array
      words = realloc(words, (sizeof(*words) + counter) * sizeof(WordArray));  
    }
  }

  // Sort the words to find most frequent words
  qsort(words, counter, sizeof(WordArray), compareWords);
  // Store the 3 more frequent words as the result, as a single string and then print that string
  snprintf(result, 10000, "%s %d %s %s %s", fileName, counter, words[0].word, words[1].word, words[2].word);
  fclose(file);
  printf("%s\n", resultado);

}

int main(int argc, char *argv[]){
  
  // Declare threads and default attributes
  pthread_t threads[argc-1];
  pthread_attr_t attr;
  pthread_attr_init(&attr);

  // Run all threads concurrently
  int i;
  for (i = 1; i < argc; i++){
    char* arguments = (char*)malloc(sizeof(argv[i])+1);
    arguments = argv[i];
    // Create a new thread for every argument passed in by the user, and count word frequency for each
    pthread_create(&threads[i], &attr, (void*) countFrequency, (void*) arguments);
  }
  for (i = 1; i < argc; i++){
    // Join threads to avoid memory leaks
    pthread_join(threads[i], NULL);
  }

  return 0;
}



###  SERVIDORES_DHCP

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

typedef struct {
  char word[101];
  int frequency;
} WordArray ;

int compareWords(const void *f1, const void *f2){
  WordArray *a = (WordArray *)f1;
  WordArray *b = (WordArray *)f2;
  return (b->frequency - a->frequency);
}

void countFrequency(void *arg){
  
  char *fileName = (char*)malloc(sizeof(char));
  fileName = (char*)arg;
  WordArray *words = (WordArray*)calloc((1000),sizeof(WordArray));
  char *result = (char*)malloc(sizeof(result)*100);
  int counter = 0;
  int isUnique;
  int i = 0;
  FILE *file;
  char buff[1000];

  // Clear the array, so threads don't modify the program after they've been created
  for (i = 0; i < sizeof(WordArray); i++){
    words[i].word[0] = '\0';
    words[i].frequency = 0;
  }

  file = fopen(fileName, "r");
  if (file == NULL){
    printf("Couldn't open file: ");
  }
      
  else {
    while ( (fscanf(file, "%s", buff)) != EOF)
    {
      isUnique = -1;

      // String comparison - to check if the word is already in the array
      int k;
      for (k = 0; k < counter; k++){
        if (strcmp(words[k].word, buff) == 0){
          isUnique = k;
        }
      }
      // If the string is not in the array, put it in the array
      if (isUnique == -1){
        strcpy(words[counter].word, buff);
        words[counter].frequency = 1;
        counter++;
      }
      // Increase frequency of non-unique words
      else {
        words[isUnique].frequency++;
      }
      // Re-allocate memory for the array
      words = realloc(words, (sizeof(*words) + counter) * sizeof(WordArray));  
    }
  }

  // Sort the words to find most frequent words
  qsort(words, counter, sizeof(WordArray), compareWords);
  // Store the 3 more frequent words as the result, as a single string and then print that string
  snprintf(result, 10000, "%s %d %s %s %s", fileName, counter, words[0].word, words[1].word, words[2].word);
  fclose(file);
  printf("%s\n", resultado);

}

int main(int argc, char *argv[]){
  
  // Declare threads and default attributes
  pthread_t threads[argc-1];
  pthread_attr_t attr;
  pthread_attr_init(&attr);

  // Run all threads concurrently
  int i;
  for (i = 1; i < argc; i++){
    char* arguments = (char*)malloc(sizeof(argv[i])+1);
    arguments = argv[i];
    // Create a new thread for every argument passed in by the user, and count word frequency for each
    pthread_create(&threads[i], &attr, (void*) countFrequency, (void*) arguments);
  }
  for (i = 1; i < argc; i++){
    // Join threads to avoid memory leaks
    pthread_join(threads[i], NULL);
  }

  return 0;
}
