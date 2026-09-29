# Atividade Remota — Máquinas de Turing
**Disciplina:** Teoria da Computação  
**Professora:** Kadidja Valéria  
**Tema:** Máquinas de Turing, Computabilidade e Limites Computacionais  
**Modalidade:** Remota | **Valor:** 1,0 ponto  

---

## 🎯 1. Objetivos da Atividade
Ao final desta atividade, o estudante deverá ser capaz de:
- Compreender o conceito de Máquina de Turing.
- Identificar os principais componentes de uma Máquina de Turing.
- Compreender a importância das Máquinas de Turing para a computação.
- Construir e simular uma Máquina de Turing simples.
- Reconhecer que existem problemas que não podem ser resolvidos por algoritmos, compreendendo os limites da computação.

---

## 📚 2. Conteúdo Programático
- Conceito de Máquina de Turing.
- Fita, cabeça de leitura/escrita e estados.
- Alfabeto e regras de transição.
- Funcionamento de uma Máquina de Turing.
- Simulação computacional.
- Computabilidade e limites computacionais.

---

## 🚀 3. Desenvolvimento da Atividade

### **Etapa 1 - Introdução**

1. **O que é uma Máquina de Turing?** Conforme dito pelo Fábio Akita, a máquina de Turing é um modelo matemático abstrato e universal de computação proposto por Alan Turing. Ela consiste essencialmente em uma fita de papel infinita (que serve simultaneamente como entrada, saída e espaço de armazenamento de dados/programa) e uma cabeça de leitura/escrita que pode se mover para a esquerda, para a direita ou permanecer parada, operando com base em um conjunto finito de estados e regras de transição.

2. **Quais são os principais componentes de uma Máquina de Turing?**

   * **Fita infinita:** Dividida em células ou unidades quadradas, onde cada célula pode conter um símbolo de um alfabeto específico ou um espaço em branco.

   * **Cabeça de leitura/escrita:** Um mecanismo que lê o símbolo atual na fita, pode apagar ou escrever um novo símbolo, e mover-se para a esquerda ou para a direita.

   * **Conjunto de estados finitos:** Um controle interno que determina o estado atual em que a máquina se encontra a cada momento.

   * **Função de transição:** A tabela de regras que dita, com base no estado atual e no símbolo lido, qual será o próximo estado, qual símbolo escrever e para qual direção a cabeça deve se mover.

3. **Qual é a importância das Máquinas de Turing para a computação?**

   Ela estabelece os fundamentos teóricos da ciência da computação moderna. Matematicamente, ela define formalmente o que é um algoritmo, servindo de base para o conceito de "máquina universal", que deu origem aos computadores modernos capazes de armazenar programas e dados no mesmo espaço de memória.

4. **Qual é a relação entre Máquina de Turing e algoritmo?**

   Um algoritmo é um procedimento passo a passo bem definido para resolver um problema. A Máquina de Turing formaliza esse conceito matematicamente: qualquer procedimento que possa ser executado por um algoritmo pode ser simulado por uma Máquina de Turing, e vice-versa (conforme a Tese de Church-Turing).

### **Etapa 2 e 3 - Simulação da Máquina de Turing ($0^n1^n$)**

Para resolver o desafio de reconhecer palavras da forma $0^n1^n$ (mesma quantidade de zeros seguidos pela mesma quantidade de uns), a lógica de funcionamento da máquina em um simulador (*Turing Machine Simulator*) segue o princípio de marcação de pares:

* **Descrição do funcionamento:**

  A máquina começa no estado inicial procurando pelo primeiro `0` à esquerda. Quando o encontra, ela o substitui por um símbolo de marcação (por exemplo, `X`) para indicar que foi processado. Em seguida, ela se move para a direita em direção à área dos `1`s, procurando o primeiro `1` correspondente e o substitui por outro marcador (por exemplo, `Y`). Após marcar um `0` e um `1`, a máquina retorna para a esquerda para encontrar o próximo `0` não marcado, repetindo o processo. Se todos os `0`s forem devidamente emparelhados com os `1`s e nenhum símbolo sobrar sem correspondência, a máquina entra em um estado de aceitação (`ACEITA`). Caso contrário, se sobrar algum `0` sem `1` correspondente (ou vice-versa), a execução é rejeitada (`REJEITA`).

* **Registro dos testes:**

| **Teste** | **Entrada** | **Resultado esperado** | **Resultado obtido** | **Estados percorridos**                                                                                                            |
| --------- | ----------- | ---------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **1**     | `0011`      | ACEITA                 | ACEITA               | `q0` $\rightarrow$ `escreve_X` $\rightarrow$ `procura_1` $\rightarrow$ `escreve_Y` $\rightarrow$ `retorna` $\rightarrow$ `aceita`  |
| **2**     | `000111`    | ACEITA                 | ACEITA               | `q0` $\rightarrow$ `escreve_X` $\rightarrow$ `procura_1` $\rightarrow$ `escreve_Y` $\rightarrow$ `retorna` $\rightarrow$ `aceita`  |
| **3**     | `00111`     | REJEITA                | REJEITA              | `q0` $\rightarrow$ `escreve_X` $\rightarrow$ `procura_1` $\rightarrow$ `escreve_Y` $\rightarrow$ `retorna` $\rightarrow$ `rejeita` |

> <img width="1917" height="1025" alt="print imput 00111" src="https://github.com/user-attachments/assets/ebd0f129-2234-472a-8527-2419d4e5c971" />
> <img width="1912" height="1035" alt="Print input 0011" src="https://github.com/user-attachments/assets/bf83abb6-6dee-4701-a6b7-e657ca518e7f" />
> <img width="800" height="432" alt="Print input 000111" src="https://github.com/user-attachments/assets/08f35eea-6102-4008-837c-bdb160a6218a" />


### **Etapa 4 - Reflexão sobre os limites computacionais**

Uma Máquina de Turing **não** consegue resolver qualquer problema. Existem problemas matemáticos e computucionais bem definidos que são chamados de **não computáveis** (ou indecidíveis), o que significa que nenhum algoritmo ou computador — por mais potente que seja ou por mais tempo que execute — poderá resolvê-los para todas as entradas possíveis. O exemplo mais clássico abordado na teoria é o *Problema da Parada* (Halting Problem), provado por Alan Turing, que demonstra ser impossível criar um programa geral capaz de prever se qualquer outro programa vai terminar sua execução ou entrar em um loop infinito. Isso evidencia que os limites da computação não são apenas uma questão de limitação de hardware, velocidade ou falta de otimização, mas sim barreiras matemáticas intransponíveis do que é calculável.

### **Questão Final**

Para saber se um problema complexo é apenas difícil de resolver (exigindo muitos recursos de tempo/espaço, como os problemas da classe NP) ou se ele é **indecidível** (inexistência de algoritmo), recorremos aos conceitos de computabilidade e redução formal estudados na Teoria da Computação. Se conseguirmos mapear ou transformar um problema conhecido por ser indecidível (como o *Problema da Parada*) no novo problema através de uma redução, provamos matematicamente que nenhum algoritmo no mundo poderá resolvê-lo de forma geral, pois a própria Máquina de Turing falharia diante de sua inerente não computabilidade.

