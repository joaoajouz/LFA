# Atividade Remota — Máquinas de Turing
**Disciplina:** Teoria da Computação  
**Professora:** Kadidja Valéria  
**Tema:** Máquinas de Turing, Computabilidade e Limites Computacionais  
**Modalidade:** Remota | **Valor:** 1,0 ponto  

---

## 📌 Material de Apoio Obrigatório
Antes de realizar a atividade, assista ao vídeo indicado:
- **Vídeo:** *Akitando #86 - O Computador de Turing e Von Neumann: Por que calculadoras não são computadores?*
> **Orientação:** Assista ao material com atenção e utilize os conceitos apresentados para responder às questões e desenvolver a atividade de simulação.

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

### Etapa 1 - Introdução (Questões Teóricas)
Após assistir ao vídeo e estudar o material disponibilizado, responda às questões abaixo:

Com base no vídeo do Fábio Akita e nas diretrizes da atividade apresentada no documento, organizei as respostas para cada uma das etapas do trabalho.

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

Para resolver o desafio de reconhecer palavras da forma $0^n1^n$ (mesma quantidade de zeros seguidos pela mesma quantidade de uns), a lógica de funcionamento da máquina em um simulador (como o *Turing Machine Simulator*) segue o princípio de marcação de pares:

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

---

### Etapa 2 - Simulação Computacional
Utilize um software ou simulador de Máquina de Turing (ex.: JFLAP, Turing Machine Simulator).

**Desafio:** Crie uma máquina capaz de reconhecer linguagens do tipo $0^n 1^n$ ($n \ge 1$), verificando se existe a mesma quantidade de símbolos `0` e `1` na sequência correta.

* **Exemplos aceitos:** `01`, `0011`, `000111`, `00001111`
* **Exemplos rejeitados:** `0`, `1`, `001`, `011`, `00111`

---

### Etapa 3 - Registro da Simulação
Após executar a máquina no simulador, preencha a tabela de testes e anexe as capturas de tela (screenshots) das evidências.

#### Tabela de Testes
| Teste | Entrada | Resultado Esperado | Resultado Obtido | Estados Percorridos |
| :---: | :--- | :---: | :---: | :--- |
| **1** | `0011` | ACEITA | | |
| **2** | `000111` | ACEITA | | |
| **3** | `00111` | REJEITA | | |

#### Descrição da Máquina de Turing Criada
> *Descreva brevemente como sua máquina funciona e qual lógica/alfabeto de fita foi utilizado para marcar os símbolos processados...*

#### Evidências / Screenshots
![Simulação Teste 1](path/to/screenshot1.png)
![Simulação Teste 2](path/to/screenshot2.png)
![Simulação Teste 3](path/to/screenshot3.png)

---

### Etapa 4 - Reflexão sobre os Limites Computacionais
Uma Máquina de Turing consegue resolver qualquer problema? Explique com suas palavras por que existem problemas que não podem ser resolvidos por algoritmos.  
*(Sua resposta deve ter entre 5 e 10 linhas)*

> *Sua resposta aqui...*

---

## ❓ Questão Final (Problema para Reflexão)
> Imagine que você recebeu um problema computacional muito complexo. Como saber se ele é apenas difícil de resolver ou se, na verdade, não existe nenhum algoritmo capaz de resolvê-lo para todos os casos?  
> Explique utilizando os conceitos estudados sobre Máquinas de Turing, computabilidade e limites computacionais.

> *Sua resposta aqui...*

---

## 📊 Critérios de Avaliação (1,0 ponto)

| Critério | Valor |
| :--- | :---: |
| Compreensão do conceito e importância das Máquinas de Turing | 0,20 |
| Construção/configuração da Máquina de Turing | 0,30 |
| Realização e registro da simulação | 0,20 |
| Interpretação dos resultados | 0,10 |
| Compreensão dos limites computacionais | 0,20 |
| **Total** | **1,00** |

---

## 📦 Orientações para Entrega
1. Assista ao vídeo indicado.
2. Estude os conceitos apresentados.
3. Responda às questões propostas.
4. Realize a simulação da Máquina de Turing.
5. Faça os três testes solicitados e registre os resultados.
6. Responda às reflexões sobre os limites computacionais.
7. Organize o material em um único arquivo (PDF/Word ou via repositório/Markdown) e envie conforme as orientações do professor.
