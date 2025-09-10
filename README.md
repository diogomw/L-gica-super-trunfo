#include <stdio.h>
#include <stdlib.h>
#include <time.h>

typedef struct {
    char nome[30];
    int forca;
    int velocidade;
    int estetica;
} Carta;

#define NUM_CARTAS 5

void criarCartas(Carta cartas[]) {
    Carta c1 = {"hb20", 90, 70, 60};
    Carta c2 = {"Lancer", 70, 90, 80};
    Carta c3 = {"Fiesta", 60, 60, 90};
    Carta c4 = {"Corolla", 80, 50, 40};
    Carta c5 = {"Civic", 75, 85, 70};

    cartas[0] = c1;
    cartas[1] = c2;
    cartas[2] = c3;
    cartas[3] = c4;
    cartas[4] = c5;
}

void mostrarCarta(Carta c) {
    printf("Nome: %s\n", c.nome);
    printf("1. Força: %d\n", c.forca);
    printf("2. Velocidade: %d\n", c.velocidade);
    printf("3. Estetica: %d\n", c.estetica);
}

void jogarRodada(Carta jogador, Carta computador) {
    int escolha;
    printf("\nSua carta:\n");
    mostrarCarta(jogador);

    printf("\nEscolha o atributo para competir (1-Força, 2-Velocidade, 3-Estetica): ");
    scanf("%d", &escolha);

    int valorJogador = 0, valorComputador = 0;
    switch (escolha) {
        case 1:
            valorJogador = jogador.forca;
            valorComputador = computador.forca;
            break;
        case 2:
            valorJogador = jogador.velocidade;
            valorComputador = computador.velocidade;
            break;
        case 3:
            valorJogador = jogador.estetica;
            valorComputador = computador.estetica;
            break;
        default:
            printf("Opção inválida!\n");
            return;
    }

    printf("\nCarta do computador:\n");
    mostrarCarta(computador);

    printf("\nResultado:\n");
    if (valorJogador > valorComputador)
        printf("Você venceu esta rodada!\n");
    else if (valorJogador < valorComputador)
        printf("Computador venceu esta rodada!\n");
    else
        printf("Empate!\n");
}

int main() {
    srand(time(NULL));
    Carta cartas[NUM_CARTAS];
    criarCartas(cartas);

    int indiceJogador = rand() % NUM_CARTAS;
    int indiceComputador = rand() % NUM_CARTAS;

    // Evita que ambos peguem a mesma carta
    while (indiceComputador == indiceJogador) {
        indiceComputador = rand() % NUM_CARTAS;
    }

    Carta cartaJogador = cartas[indiceJogador];
    Carta cartaComputador = cartas[indiceComputador];

    jogarRodada(cartaJogador, cartaComputador);

    return 0;
}
