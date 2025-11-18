#include <stdio.h>

#define TAM 10          // Tamanho do tabuleiro (10x10)
#define NAVIO 3         // Valor que representa partes do navio
#define TAMANHO_NAVIO 3 // Quantidade de casas ocupadas pelo navio

int main() {

    // ================== TABULEIRO ======================
    int tabuleiro[TAM][TAM];

    // Inicializa tabuleiro com água (0)
    for(int i = 0; i < TAM; i++){
        for(int j = 0; j < TAM; j++){
            tabuleiro[i][j] = 0;
        }
    }

    // ================== NAVIOS =========================
    // Ambos têm 3 posições (fixo pelo desafio)
    int navioHorizontal[TAMANHO_NAVIO] = {NAVIO, NAVIO, NAVIO};
    int navioVertical[TAMANHO_NAVIO]   = {NAVIO, NAVIO, NAVIO};

    // ==== Coordenadas iniciais dos navios (DEFINIDAS NO CÓDIGO) ====
    int linhaH = 2; // linha do navio horizontal
    int colH   = 4; // coluna inicial horizontal

    int linhaV = 5; // linha inicial navio vertical
    int colV   = 1; // coluna do navio vertical

    // ==============================================================
    // ======== VALIDAÇÃO DE LIMITES DO TABULEIRO ===================
    // ==============================================================
    if(colH + TAMANHO_NAVIO > TAM){
        printf("❌ ERRO: Navio horizontal fora dos limites!\n");
        return 1;
    }

    if(linhaV + TAMANHO_NAVIO > TAM){
        printf("❌ ERRO: Navio vertical fora dos limites!\n");
        return 1;
    }

    // ==============================================================
    // ======== VERIFICAR SE EXISTE SOBREPOSIÇÃO ====================
    // ==============================================================
    for(int i = 0; i < TAMANHO_NAVIO; i++){
        if(tabuleiro[linhaV + i][colV] != 0 ||
           tabuleiro[linhaH][colH + i] != 0){
            printf("❌ ERRO: Sobreposição detectada!\n");
            return 1;
        }
    }

    // ==============================================================
    // ========= POSICIONANDO NAVIO HORIZONTAL =======================
    // ==============================================================
    for(int i = 0; i < TAMANHO_NAVIO; i++){
        tabuleiro[linhaH][colH + i] = navioHorizontal[i];
    }

    // ========= POSICIONANDO NAVIO VERTICAL ========================
    for(int i = 0; i < TAMANHO_NAVIO; i++){
        tabuleiro[linhaV + i][colV] = navioVertical[i];
    }

    // ==============================================================
    // ================= EXIBIR O TABULEIRO =========================
    // ==============================================================
    printf("\n===== TABULEIRO BATALHA NAVAL =====\n\n");

    for(int i = 0; i < TAM; i++){
        for(int j = 0; j < TAM; j++){
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }

    printf("\nLegenda: 0 = água | 3 = navio\n");

    return 0;
}
