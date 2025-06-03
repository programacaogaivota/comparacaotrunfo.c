#include <stdio.h>
#include <string.h> // Para usar strcpy e strcmp

// 1. Definindo a estrutura para uma Carta
typedef struct {
    char estado[3];
    char codigo[4];
    char nomeCidade[30];
    int populacao;
    float area;
    float pib;
    int pontosTuristicos;
} Carta;

// Função para ler os dados de uma carta
void lerDadosCarta(Carta *carta, int numeroCarta) {
    printf("\n--- Digite os dados da Carta %d ---\n", numeroCarta);

    printf("Estado (ex: AP): ");
    scanf("%s", carta->estado);

    printf("Codigo (ex: A01): ");
    scanf("%s", carta->codigo);

    printf("Nome da cidade: ");
    scanf(" %29[^\n]", carta->nomeCidade); // Lê a linha inteira, até o ENTER

    printf("Populacao: ");
    scanf("%d", &carta->populacao);

    printf("Area (Km2): ");
    scanf("%f", &carta->area);

    printf("PIB: ");
    scanf("%f", &carta->pib);

    printf("Pontos Turisticos: ");
    scanf("%d", &carta->pontosTuristicos);
}

// Função para exibir os dados de uma carta
void exibirCarta(const Carta *carta, int numeroCarta) {
    printf("\n--- Dados da Carta %d ---\n", numeroCarta);
    printf("Estado: %s\n", carta->estado);
    printf("Codigo: %s\n", carta->codigo);
    printf("Cidade: %s\n", carta->nomeCidade);
    printf("Populacao: %d\n", carta->populacao);
    printf("Area: %.3f Km2\n", carta->area);
    printf("PIB: %.8f\n", carta->pib);
    printf("Pontos Turisticos: %d\n", carta->pontosTuristicos);
}

// Função para comparar duas cartas com base em um atributo
// Retorna: 1 se carta1 ganha, 2 se carta2 ganha, 0 se empate
int compararCartas(const Carta *carta1, const Carta *carta2, const char *atributo) {
    printf("\n--- Comparando pelo atributo: %s ---\n", atributo);

    if (strcmp(atributo, "populacao") == 0) {
        if (carta1->populacao > carta2->populacao) return 1;
        if (carta2->populacao > carta1->populacao) return 2;
    } else if (strcmp(atributo, "area") == 0) {
        if (carta1->area > carta2->area) return 1;
        if (carta2->area > carta1->area) return 2;
    } else if (strcmp(atributo, "pib") == 0) {
        if (carta1->pib > carta2->pib) return 1;
        if (carta2->pib > carta1->pib) return 2;
    } else if (strcmp(atributo, "pontosTuristicos") == 0) {
        if (carta1->pontosTuristicos > carta2->pontosTuristicos) return 1;
        if (carta2->pontosTuristicos > carta1->pontosTuristicos) return 2;
    } else {
        printf("Atributo '%s' invalido para comparacao.\n", atributo);
        return 0; // Atributo inválido
    }
    return 0; // Empate
}


int main() {
    printf("Desafio Super Trunfo!\n\n");

    Carta carta1; // Declara uma variável do tipo Carta
    Carta carta2; // Declara outra variável do tipo Carta

    // Preenche os dados da Carta 1
    lerDadosCarta(&carta1, 1);
    exibirCarta(&carta1, 1);

    // Preenche os dados da Carta 2
    lerDadosCarta(&carta2, 2);
    exibirCarta(&carta2, 2);

    char atributoParaComparar[30];
    printf("\nQual atributo voce quer comparar? (populacao, area, pib, pontosTuristicos): ");
    scanf("%s", atributoParaComparar);

    int resultado = compararCartas(&carta1, &carta2, atributoParaComparar);

    printf("\n--- Resultado da Rodada ---\n");
    if (resultado == 1) {
        printf("A Carta 1 (%s) ganhou a rodada!\n", carta1.nomeCidade);
    } else if (resultado == 2) {
        printf("A Carta 2 (%s) ganhou a rodada!\n", carta2.nomeCidade);
    } else {
        printf("A rodada empatou ou o atributo eh invalido!\n");
    }

    return 0;
}
