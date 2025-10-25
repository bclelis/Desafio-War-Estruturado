/*
 * PROJETO: War Estruturado (Desafio Níveis 1, 2 e 3)
 * LINGUAGEM: C
 *
 * DESCRIÇÃO: Este programa simula elementos básicos do jogo War.
 * Nível 1: Define a estrutura 'Territorio' e implementa cadastro e exibição.
 * Nível 2: Adiciona alocação dinâmica para o mapa e a função 'atacar' 
 * com ponteiros e lógica de dados (rand).
 * Nível 3: Implementa um sistema de missões estratégicas dinâmicas 
 * para dois jogadores (Azul e Vermelho).
 */

// Bibliotecas necessárias (Níveis 1, 2 e 3)
#include <stdio.h>
#include <stdlib.h> // Para malloc, calloc, free, rand, srand
#include <string.h> // Para strcpy, strcmp
#include <time.h>   // Para time() (seed do rand)

// --- NÍVEL 1: Definição da Struct ---

/*
 * Estrutura Territorio
 * Agrupa os dados de um território do jogo.
 */
typedef struct {
    char nome[30];
    char cor[10]; // Cor do exército que o domina
    int tropas;
} Territorio;


// --- NÍVEL 3: Definição do Vetor de Missões ---

/*
 * Vetor global de missões (strings)
 * Contém as descrições das missões possíveis.
 */
const char* missoes[] = {
    "Controlar 4 territorios",
    "Eliminar a cor 'Vermelho'",
    "Eliminar a cor 'Azul'",
    "Eliminar a cor 'Verde'",
    "Possuir 10 tropas em um territorio"
};
// Calcula o número total de missões automaticamente
const int totalMissoes = sizeof(missoes) / sizeof(missoes[0]);


// --- PROTÓTIPOS DAS FUNÇÕES (Modularização) ---

// Funções dos Níveis 1 e 2
void cadastrarTerritorios(Territorio* mapa, int tamanho);
void exibirTerritorios(Territorio* mapa, int tamanho);

// Funções do Nível 2
void atacar(Territorio* atacante, Territorio* defensor);
void liberarMemoria(Territorio* mapa, char* missaoJ1, char* missaoJ2);

// Funções do Nível 3
void atribuirMissao(char* destino, const char* missoes[], int totalMissoes);
int verificarMissao(const char* missao, Territorio* mapa, int tamanho, const char* corJogador);


// --- FUNÇÃO PRINCIPAL (main) ---

int main() {
    int numTerritorios;
    Territorio* mapa = NULL; // Ponteiro para o mapa (Nível 2)
    char* missaoJogadorAzul = NULL; // Missão do Jogador 1 (Nível 3)
    char* missaoJogadorVermelho = NULL; // Missão do Jogador 2 (Nível 3)
    char continuarAtaque = 's';
    int vencedor = 0; // 0 = Ninguém, 1 = Azul, 2 = Vermelho

    // Nível 2: Inicializa o gerador de números aleatórios
    srand(time(NULL));

    printf("--- WAR ESTRUTURADO (Niveis 1, 2 e 3) ---\n\n");

    // --- NÍVEL 2: Alocação Dinâmica ---
    printf("Quantos territorios existem no mapa? ");
    scanf("%d", &numTerritorios);

    // Validação simples
    if (numTerritorios < 2) {
        printf("Erro: O mapa precisa de pelo menos 2 territorios.\n");
        return 1;
    }

    // Aloca memória para o vetor de territórios (usando calloc)
    mapa = (Territorio*) calloc(numTerritorios, sizeof(Territorio));
    if (mapa == NULL) {
        printf("Erro: Falha na alocacao de memoria para o mapa.\n");
        return 1;
    }

    // --- NÍVEL 3: Alocação Dinâmica das Missões ---
    // Aloca espaço para armazenar a string da missão de cada jogador
    missaoJogadorAzul = (char*) malloc(100 * sizeof(char));
    missaoJogadorVermelho = (char*) malloc(100 * sizeof(char));

    if (missaoJogadorAzul == NULL || missaoJogadorVermelho == NULL) {
        printf("Erro: Falha na alocacao de memoria para as missoes.\n");
        // Libera o que já foi alocado antes de sair
        if (mapa) free(mapa);
        if (missaoJogadorAzul) free(missaoJogadorAzul);
        if (missaoJogadorVermelho) free(missaoJogadorVermelho);
        return 1;
    }

    // --- NÍVEL 1: Cadastro dos Territórios ---
    cadastrarTerritorios(mapa, numTerritorios);

    // --- NÍVEL 3: Atribuição das Missões ---
    atribuirMissao(missaoJogadorAzul, missoes, totalMissoes);
    atribuirMissao(missaoJogadorVermelho, missoes, totalMissoes);

    printf("\n--- Missoes Estrategicas Distribuidas ---\n");
    printf("Jogador 'Azul': %s\n", missaoJogadorAzul);
    printf("Jogador 'Vermelho': %s\n", missaoJogadorVermelho);

    // --- NÍVEL 2 e 3: Loop Principal do Jogo (Ataques e Verificação) ---
    while (vencedor == 0) {
        
        // Nível 1: Exibição dos dados
        printf("\n--- ESTADO ATUAL DO MAPA ---\n");
        exibirTerritorios(mapa, numTerritorios);

        // Nível 3: Verificação de Missão (Início do turno)
        if (verificarMissao(missaoJogadorAzul, mapa, numTerritorios, "Azul")) {
            vencedor = 1;
            break;
        }
        if (verificarMissao(missaoJogadorVermelho, mapa, numTerritorios, "Vermelho")) {
            vencedor = 2;
            break;
        }

        printf("\nDeseja realizar um ataque? (s/n): ");
        // O espaço antes de %c ignora quebras de linha (newlines) pendentes
        scanf(" %c", &continuarAtaque);

        if (continuarAtaque != 's' && continuarAtaque != 'S') {
            break; // Termina o jogo se o usuário não quiser atacar
        }

        // Lógica de Ataque (Nível 2)
        int idxAtacante, idxDefensor;
        char corTurno[10];
        int turnoJogador;

        printf("Qual jogador ataca? (1 = Azul, 2 = Vermelho): ");
        scanf("%d", &turnoJogador);
        strcpy(corTurno, (turnoJogador == 1) ? "Azul" : "Vermelho");

        printf("Digite o ID (indice) do territorio ATACANTE: ");
        scanf("%d", &idxAtacante);
        printf("Digite o ID (indice) do territorio DEFENSOR: ");
        scanf("%d", &idxDefensor);

        // Validações
        if (idxAtacante < 0 || idxAtacante >= numTerritorios ||
            idxDefensor < 0 || idxDefensor >= numTerritorios) {
            printf("Erro: ID de territorio invalido.\n");
            continue;
        }

        // Validação de posse (Nível 3)
        if (strcmp(mapa[idxAtacante].cor, corTurno) != 0) {
            printf("Erro: O jogador %s nao controla o territorio atacante!\n", corTurno);
            continue;
        }

        // Validação de ataque (Nível 2)
        if (strcmp(mapa[idxAtacante].cor, mapa[idxDefensor].cor) == 0) {
            printf("Erro: Nao pode atacar um territorio da propria cor!\n");
            continue;
        }

        // Validação de tropas
        if (mapa[idxAtacante].tropas <= 1) {
            printf("Erro: O territorio atacante precisa de mais de 1 tropa para atacar.\n");
            continue;
        }

        // Executa o ataque (passando ponteiros)
        printf("\n--- SIMULACAO DE BATALHA ---\n");
        atacar(&mapa[idxAtacante], &mapa[idxDefensor]);
    }

    // --- FIM DO JOGO ---
    printf("\n--- JOGO FINALIZADO ---\n");
    if (vencedor == 1) {
        printf("VITORIA! O Jogador 'Azul' cumpriu sua missao!\n");
    } else if (vencedor == 2) {
        printf("VITORIA! O Jogador 'Vermelho' cumpriu sua missao!\n");
    } else {
        printf("O jogo terminou sem um vencedor por missao.\n");
    }

    printf("Estado final do mapa:\n");
    exibirTerritorios(mapa, numTerritorios);

    // --- NÍVEL 2 e 3: Gerenciamento de Memória ---
    liberarMemoria(mapa, missaoJogadorAzul, missaoJogadorVermelho);
    printf("\nMemoria liberada com sucesso.\n");

    return 0;
}


// --- IMPLEMENTAÇÃO DAS FUNÇÕES ---

/**
 * Nível 1: Cadastro dos Territórios
 * Preenche o vetor de territórios dinamicamente alocado.
 */
void cadastrarTerritorios(Territorio* mapa, int tamanho) {
    printf("\n--- Cadastro de Territorios (Nivel 1) ---\n");
    printf("Instrucao: Cadastre os territorios iniciais (cores: Azul, Vermelho, Verde, etc.)\n");

    for (int i = 0; i < tamanho; i++) {
        printf("\n--- Territorio %d ---\n", i);
        
        printf("Nome: ");
        // Limita a leitura para evitar overflow (29 caracteres + \0)
        scanf("%29s", (mapa + i)->nome); 

        printf("Cor do Exercito: ");
        scanf("%9s", (mapa + i)->cor);

        printf("Quantidade de Tropas: ");
        scanf("%d", &(mapa + i)->tropas);
    }
}

/**
 * Nível 1: Exibição dos Dados
 * Mostra o estado atual de todos os territórios no mapa.
 */
void exibirTerritorios(Territorio* mapa, int tamanho) {
    printf("--------------------------------------------------\n");
    for (int i = 0; i < tamanho; i++) {
        // Usando a notação de ponteiro (mapa + i) -> campo
        printf("ID: %d | Nome: %-15s | Cor: %-10s | Tropas: %d\n",
               i,
               (mapa + i)->nome,
               (mapa + i)->cor,
               (mapa + i)->tropas);
    }
    printf("--------------------------------------------------\n");
}

/**
 * Nível 2: Simulação de Ataque
 * Simula uma batalha entre dois territórios usando ponteiros.
 */
void atacar(Territorio* atacante, Territorio* defensor) {
    // Simula rolagem de dados (1 a 6)
    int dadoAtacante = (rand() % 6) + 1;
    int dadoDefensor = (rand() % 6) + 1;

    printf("Atacante (%s) rolou: %d\n", atacante->nome, dadoAtacante);
    printf("Defensor (%s) rolou: %d\n", defensor->nome, dadoDefensor);

    // Compara os dados (ataque vence em empates)
    if (dadoAtacante > dadoDefensor) {
        // Atacante vence
        printf("VITORIA DO ATAQUE! %s conquistou %s!\n", atacante->nome, defensor->nome);

        // Calcula tropas a mover (metade das tropas do atacante, exceto 1)
        int tropasMovidas = (atacante->tropas - 1) / 2;
        if (tropasMovidas < 1) {
            tropasMovidas = 1; // Deve mover pelo menos 1
        }

        // Atualiza o território defensor (que foi conquistado)
        strcpy(defensor->cor, atacante->cor); // Muda a cor
        defensor->tropas = tropasMovidas;       // Recebe as tropas movidas

        // Atualiza o território atacante
        atacante->tropas = atacante->tropas - tropasMovidas;

    } else {
        // Defensor vence
        printf("VITORIA DA DEFESA! %s repeliu o ataque.\n", defensor->nome);
        
        // Atacante perde 1 tropa (conforme requisito)
        atacante->tropas = atacante->tropas - 1;
        if (atacante->tropas < 1) {
            atacante->tropas = 1; // Garante que o território não fique com 0
        }
    }
}

/**
 * Nível 3: Atribuição de Missão
 * Sorteia uma missão do vetor global e a copia para o destino.
 */
void atribuirMissao(char* destino, const char* missoes[], int totalMissoes) {
    // Sorteia um índice aleatório
    int indiceSorteado = rand() % totalMissoes;
    
    // Copia a string da missão sorteada para o ponteiro de destino
    strcpy(destino, missoes[indiceSorteado]);
}

/**
 * Nível 3: Verificação de Missão
 * Verifica se a condição de vitória de uma missão foi atingida.
 * (Implementação com lógica simples, conforme solicitado)
 */
int verificarMissao(const char* missao, Territorio* mapa, int tamanho, const char* corJogador) {
    int i;
    int contagemTerritoriosJogador = 0;
    int contagemTropasMax = 0;
    
    // Cálculos comuns: contar territórios e tropas do jogador
    for (i = 0; i < tamanho; i++) {
        if (strcmp(mapa[i].cor, corJogador) == 0) {
            contagemTerritoriosJogador++;
            if (mapa[i].tropas > contagemTropasMax) {
                contagemTropasMax = mapa[i].tropas;
            }
        }
    }

    // --- Lógica de Verificação ---
    
    // Missão: "Controlar 4 territorios"
    if (strcmp(missao, "Controlar 4 territorios") == 0) {
        return (contagemTerritoriosJogador >= 4);
    }
    
    // Missão: "Eliminar a cor 'Vermelho'"
    else if (strcmp(missao, "Eliminar a cor 'Vermelho'") == 0) {
        if (strcmp(corJogador, "Vermelho") == 0) return 0; // Não pode eliminar a si mesmo
        for (i = 0; i < tamanho; i++) {
            if (strcmp(mapa[i].cor, "Vermelho") == 0) {
                return 0; // Se encontrar 1, a missão não foi cumprida
            }
        }
        return 1; // Se o loop terminar, a cor foi eliminada
    }
    
    // Missão: "Eliminar a cor 'Azul'"
    else if (strcmp(missao, "Eliminar a cor 'Azul'") == 0) {
        if (strcmp(corJogador, "Azul") == 0) return 0;
        for (i = 0; i < tamanho; i++) {
            if (strcmp(mapa[i].cor, "Azul") == 0) {
                return 0;
            }
        }
        return 1;
    }
    
    // Missão: "Eliminar a cor 'Verde'"
    else if (strcmp(missao, "Eliminar a cor 'Verde'") == 0) {
        if (strcmp(corJogador, "Verde") == 0) return 0;
        for (i = 0; i < tamanho; i++) {
            if (strcmp(mapa[i].cor, "Verde") == 0) {
                return 0;
            }
        }
        return 1;
    }

    // Missão: "Possuir 10 tropas em um territorio"
    else if (strcmp(missao, "Possuir 10 tropas em um territorio") == 0) {
        return (contagemTropasMax >= 10);
    }

    return 0; // Nenhuma missão correspondente ou cumprida
}

/**
 * Nível 2 e 3: Liberação de Memória
 * Libera toda a memória alocada dinamicamente (mapa e missões).
 */
void liberarMemoria(Territorio* mapa, char* missaoJ1, char* missaoJ2) {
    // Documentação: É crucial liberar a memória na ordem inversa
    // ou garantir que todos os ponteiros alocados sejam liberados
    // para evitar 'memory leaks'.
    
    if (mapa != NULL) {
        free(mapa); // Libera o vetor de territórios (Nível 2)
    }
    if (missaoJ1 != NULL) {
        free(missaoJ1); // Libera a string da missão 1 (Nível 3)
    }
    if (missaoJ2 != NULL) {
        free(missaoJ2); // Libera a string da missão 2 (Nível 3)
    }
}
