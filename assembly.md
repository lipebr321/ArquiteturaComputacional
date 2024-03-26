# Introdução à Linguagem Assembly

## O que é Linguagem Assembly?

A linguagem Assembly é uma linguagem de baixo nível usada para programar sistemas computacionais diretamente. Ao contrário das linguagens de alto nível, como C++ ou Python, que são projetadas para serem facilmente compreensíveis pelos humanos, a linguagem Assembly é altamente legível pelos computadores.

## Como Funciona?

A linguagem Assembly é composta por um conjunto de instruções mnemônicas que correspondem diretamente às instruções de máquina executadas pelo processador. Cada instrução Assembly é traduzida diretamente em uma sequência de bits que o processador pode entender e executar.

## Por que Usar Assembly?

Embora seja mais complexa e tediosa de escrever em comparação com linguagens de alto nível, como C ou Python, a linguagem Assembly oferece controle direto sobre o hardware do computador e pode ser altamente otimizada para desempenho. É comumente usada em situações onde o desempenho é crítico, como em sistemas embarcados, drivers de dispositivo e programação de baixo nível.

## Estrutura de um Programa Assembly

Um programa escrito em Assembly é composto por uma série de instruções Assembly, que são organizadas em seções específicas do programa. As seções comuns em um programa Assembly incluem:

- **Seção de Dados**: Onde variáveis e constantes são definidas.
- **Seção de Texto**: Onde as instruções do programa são escritas.
- **Seção de Inicialização**: Onde o programa começa sua execução.

## Exemplo Simples

Aqui está um exemplo simples de um programa Assembly que imprime "Hello, World!" na tela:

Vamos analisar o exemplo de código em Assembly linha por linha:

```assembly
section .text
    global _start

_start:
    ; Escrever "Hello, world!" na saída padrão
    mov     eax, 4            ; Número da chamada do sistema para sys_write
    mov     ebx, 1            ; Descritor de arquivo para stdout
    mov     ecx, msg          ; Endereço da mensagem
    mov     edx, msg.len      ; Comprimento da mensagem
    int     0x80              ; Chamada do sistema

    ; Sair do programa
    mov     eax, 1            ; Número da chamada do sistema para sys_exit
    xor     ebx, ebx          ; Código de retorno 0
    int     0x80              ; Chamada do sistema

section .data
    msg     db  'Hello, world!', 0xA  ; Mensagem a ser exibida
    len     equ $ - msg                ; Comprimento da mensagem


```

## Explicação do Código em Assembly

### Seção `.text`

- `section .text`: Esta linha declara a seção de código do programa, onde as instruções executáveis são definidas.
- `global _start`: Define o ponto de entrada do programa como `_start`, que é o ponto onde a execução do programa começa.

### Ponto de Entrada (`_start`)

- `mov eax, 4`: Move o número da chamada do sistema `sys_write` para o registrador `eax`. Essa chamada do sistema é usada para escrever na saída padrão.
- `mov ebx, 1`: Move o descritor de arquivo para a saída padrão (stdout) para o registrador `ebx`.
- `mov ecx, msg`: Move o endereço da mensagem para o registrador `ecx`.
- `mov edx, msg.len`: Move o comprimento da mensagem para o registrador `edx`.
- `int 0x80`: Chama a interrupção do sistema (`int 0x80`), que efetua a chamada do sistema `sys_write` para escrever a mensagem na saída padrão.

### Finalização do Programa

- `mov eax, 1`: Move o número da chamada do sistema `sys_exit` para o registrador `eax`. Essa chamada do sistema é usada para encerrar o programa.
- `xor ebx, ebx`: Realiza uma operação XOR com o registrador `ebx`, definindo o código de retorno do programa como 0.
- `int 0x80`: Chama a interrupção do sistema (`int 0x80`), que efetua a chamada do sistema `sys_exit` para finalizar o programa.

### Seção `.data`

- `msg db 'Hello, world!', 0xA`: Define a mensagem a ser exibida na saída padrão. O caractere `0xA` representa uma nova linha.
- `len equ $ - msg`: Calcula o comprimento da mensagem subtraindo o endereço atual (`$`) do endereço da mensagem (`msg`).

Este exemplo ilustra como escrever um programa simples em Assembly para exibir "Hello, world!" na saída padrão e finalizar o programa. Cada instrução Assembly corresponde a uma operação específica realizada pelo processador.
