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

1. **O que é uma Máquina de Turing?**
   > *Sua resposta aqui...*

2. **Quais são os principais componentes de uma Máquina de Turing?**
   > *Sua resposta aqui...*

3. **Qual é a importância das Máquinas de Turing para a computação?**
   > *Sua resposta aqui...*

4. **Qual é a relação entre Máquina de Turing e algoritmo?**
   > *Sua resposta aqui...*

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