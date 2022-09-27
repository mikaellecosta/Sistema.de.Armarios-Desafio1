# 🧮 Sistema de Armários IFCE
Imagine que você foi contratado para desenvolver um sistema para gerenciar os armários de alunos de uma universidade. 

Inicialmente, você terá que fazer uma prova de conceito para 8 armários. Devido as limitações de memória no dispositivo onde seu código será embarcado, você optou por utilizar um mapa de bits. 

Dessa forma, para cada armário você irá associar um bit, sendo 0 para disponível e 1 para ocupado. 
Você deverá usar uma UNICA variável do tipo char sem sinal para controle. 

O sistema funcionar ́a da seguinte forma: Inicialmente, você deve exibir um menu para o usuário com
as seguintes opções:
1. Ocupar armário
2. Liberar armário
3. Sair

O programa deve iniciar com todos os armários desocupados.
- Sempre que o usuário digitar a opção 1, você deve escolher um armário aleatoriamente dentre os disponíveis e ocupar, ou seja, colocar o bit correspondente na variável de controle em 1. 
- Quando o usuário digitar a opção 2, o programa deve pedir a posição do armário para ser desocupado e colocar o bit correspondente em zero na variável de controle. 
- O programa deve sair quando a opção 3 for a escolhida pelo usuário.

## 🔎 Demonstração:

![image](https://user-images.githubusercontent.com/98134696/192402454-2f55fa75-4c66-4527-91ab-1ed17a26f20a.png)

## 👩🏻‍💻 Código:
```c
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#include <time.h>
#include <unistd.h>

int main() {
  int posicao, escolha, total;
  unsigned char armario = 0;

  total = pow(2,7);
  srand(time(NULL)); 
do{
  puts("\nEscolha um número para prosseguir: ");
  printf("1 -> ocupar armário\n2 -> liberar armário\n3 -> sair\n");
  scanf("%d",&escolha);
  switch(escolha){
    case 1:
      if(armario == 255){
        printf("Não há armário disponivel!\n");
        break;
      }
      else{ 
    do{
      posicao = rand() % 8;
    }while((armario & (int)pow(2, posicao)) != 0);  
    
    armario |= (int)pow(2, posicao);
    printf("Armário ocupado: %d\n", armario);
        }
    break;
    
      case 2:
      printf("Qual armário quer desocupar? Digite a posição: \n");
      scanf("%d", &posicao);
      if (armario * (int)pow(2,posicao) == 0){
        printf("O armário já está desocupado.\n");
      } else {
        armario &= ~(int)pow(2, posicao);
        printf("O armário foi desocupado.\n");
      }
      break;
      case 3:
      printf("O programa será encerrado!\n");
      break;  
  }

  for(int i = 0; i <= 7; i++){
    posicao = pow(2, i);
    printf((armario & posicao)? "Ø " : " %d ", i);
}
  printf("\n");
  // sleep(3);
  // system("clear");
  }while(escolha != 3);
  
  return 0;
   }
```



