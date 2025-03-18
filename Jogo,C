#include <stdio.h>
#include <stdlib.h>
#include <time.h>

char tabuleiro[3][3];
const char JOGADOR = 'X';
const char MAQUINA = 'O';

void inicializarTabuleiro() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            tabuleiro[i][j] = ' ';
        }
    }
}

void imprimirTabuleiro() {
    for (int i = 0; i < 3; i++) {
        printf(" %c | %c | %c \n", tabuleiro[i][0], tabuleiro[i][1], tabuleiro[i][2]);
        if (i < 2) printf("---|---|---\n");
    }
}

int verificarEspacosVazios() {
    int contador = 0;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (tabuleiro[i][j] == ' ') contador++;
        }
    }
    return contador;
}

char verificarVencedor() {
    for (int i = 0; i < 3; i++) {
        if (tabuleiro[i][0] != ' ' && tabuleiro[i][0] == tabuleiro[i][1] && tabuleiro[i][1] == tabuleiro[i][2])
            return tabuleiro[i][0];
        if (tabuleiro[0][i] != ' ' && tabuleiro[0][i] == tabuleiro[1][i] && tabuleiro[1][i] == tabuleiro[2][i])
            return tabuleiro[0][i];
    }
    if (tabuleiro[0][0] != ' ' && tabuleiro[0][0] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][2])
        return tabuleiro[0][0];
    if (tabuleiro[0][2] != ' ' && tabuleiro[0][2] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][0])
        return tabuleiro[0][2];
    return ' ';
}

int minimax(int profundidade, int maximizando) {
    char vencedor = verificarVencedor();
    if (vencedor == MAQUINA) return 10 - profundidade;
    if (vencedor == JOGADOR) return profundidade - 10;
    if (verificarEspacosVazios() == 0) return 0;

    int melhorPontuacao = maximizando ? -1000 : 1000;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (tabuleiro[i][j] == ' ') {
                tabuleiro[i][j] = maximizando ? MAQUINA : JOGADOR;
                int pontuacao = minimax(profundidade + 1, !maximizando);
                tabuleiro[i][j] = ' ';
                melhorPontuacao = maximizando ? (pontuacao > melhorPontuacao ? pontuacao : melhorPontuacao)
                                             : (pontuacao < melhorPontuacao ? pontuacao : melhorPontuacao);
            }
        }
    }
    return melhorPontuacao;
}

void jogadaMaquina() {
    int melhorPontuacao = -1000, x = -1, y = -1;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (tabuleiro[i][j] == ' ') {
                tabuleiro[i][j] = MAQUINA;
                int pontuacao = minimax(0, 0);
                tabuleiro[i][j] = ' ';
                if (pontuacao > melhorPontuacao) {
                    melhorPontuacao = pontuacao;
                    x = i;
                    y = j;
                }
            }
        }
    }
    if (x != -1 && y != -1) tabuleiro[x][y] = MAQUINA;
}

void jogadaJogador() {
    int x, y;
    do {
        printf("Digite a linha (1-3) e a coluna (1-3): ");
        scanf("%d %d", &x, &y);
        x--; y--;
    } while (x < 0 || x >= 3 || y < 0 || y >= 3 || tabuleiro[x][y] != ' ');
    tabuleiro[x][y] = JOGADOR;
}

void imprimirVencedor(char vencedor) {
    if (vencedor == JOGADOR) printf("Parabéns, você venceu!\n");
    else if (vencedor == MAQUINA) printf("A máquina venceu. Tente novamente!\n");
    else printf("Deu empate!\n");
}

int main() {
    inicializarTabuleiro();
    char vencedor;
    while ((vencedor = verificarVencedor()) == ' ' && verificarEspacosVazios() > 0) {
        imprimirTabuleiro();
        jogadaJogador();
        if ((vencedor = verificarVencedor()) != ' ' || verificarEspacosVazios() == 0) break;
        jogadaMaquina();
    }
    imprimirTabuleiro();
    imprimirVencedor(vencedor);
    return 0;
}
