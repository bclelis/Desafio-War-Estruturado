*War Estruturado em C (Desafio Níveis 1-3)*

Este projeto é uma simulação simplificada do jogo de tabuleiro War, implementada na linguagem C. O código foi desenvolvido de forma incremental, abrangendo três níveis de complexidade, introduzindo conceitos fundamentais de programação estruturada, gerenciamento de memória e lógica de jogo.

🚀 Funcionalidades:

O programa simula um mapa de jogo onde dois jogadores ("Azul" e "Vermelho") competem para atingir objetivos estratégicos.

Nível 1 (Fundação):

Utilização de structs (Territorio) para agrupar dados (nome, cor, tropas).

Cadastro de um número fixo (ou dinâmico) de territórios.

Exibição formatada do estado do mapa.

Nível 2 (Interatividade):

Alocação Dinâmica: O tamanho do mapa (número de territórios) é definido pelo usuário no início, utilizando calloc.

Ponteiros: Toda a manipulação do mapa é feita através de ponteiros.

Função de Ataque: Implementa a função void atacar(Territorio* atacante, Territorio* defensor) que:

Simula uma rolagem de dados (rand()) para ataque e defesa.

Atualiza as tropas e a posse (cor) do território com base no resultado da batalha.

Gerenciamento de Memória: Utiliza free() para liberar a memória alocada ao final do jogo.

Nível 3 (Estratégia):

Sistema de Missões: Define um vetor global de missões estratégicas (ex: "Eliminar a cor 'Vermelho'").

Alocação Dinâmica de Strings: As missões de cada jogador são armazenadas em memória alocada dinamicamente (malloc).

Atribuição Aleatória: Cada jogador recebe uma missão aleatória no início do jogo.

Verificação de Vitória: A cada turno, o sistema verifica se algum jogador cumpriu sua missão e declara o vencedor.

🛠️ Como Compilar e Executar:

Este projeto foi escrito em C padrão e pode ser compilado com qualquer compilador C moderno, como o gcc.

Salve o Código: Salve o código fornecido em um arquivo chamado war.c.

Abra seu Terminal: Navegue até o diretório onde você salvou o arquivo.

Compile o Programa: Execute o seguinte comando para compilar:

  gcc war.c -o war
  gcc: O compilador.

war.c: O seu arquivo fonte.

-o war: Especifica o nome do arquivo executável de saída (você pode escolher outro nome).

Execute o Jogo: Após a compilação bem-sucedida, execute o programa:

./war

(No Windows, você pode simplesmente digitar war.exe ou war no CMD/PowerShell).

Siga as Instruções: O programa solicitará primeiro o número de territórios no mapa. Em seguida, pedirá os dados de cada território (nome, cor inicial, tropas). Por fim, o jogo entrará no loop de ataque, onde você poderá simular batalhas e verificar as condições de vitória.

📁 Estrutura do Código:

O código é modularizado para facilitar a leitura e manutenção:

struct Territorio: Define o tipo de dado base do jogo.

main(): Controla o fluxo principal do jogo (setup, loop de jogo, verificação de vitória e limpeza).

cadastrarTerritorios(Territorio* mapa, int tamanho): Preenche os dados iniciais do mapa.

exibirTerritorios(Territorio* mapa, int tamanho): Mostra o estado atual de todos os territórios.

atacar(Territorio* atacante, Territorio* defensor): Executa a lógica de batalha entre dois territórios.

atribuirMissao(char* destino, const char* missoes[], int totalMissoes): Sorteia e copia uma missão para o jogador.

verificarMissao(const char* missao, Territorio* mapa, int tamanho, const char* corJogador): Verifica se a condição de vitória de um jogador foi atingida.

liberarMemoria(Territorio* mapa, char* missaoJ1, char* missaoJ2): Libera toda a memória alocada dinamicamente (mapa e as missões).
