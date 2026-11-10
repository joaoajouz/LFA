# Sistema Especialista de Crédito Responsável: Prevenção ao Superendividamento por Apostas Online (Bets)

**Disciplina:** Inteligência Artificial e Linguagens Formais e Autômatos (IA/LFA)
**Professora:** Kadidja Valéria
**Área:** Finanças, triagem de crédito responsável
**Linguagem:** Python 3 (biblioteca padrão, sem dependências)
**Inferência:** encadeamento para trás (*backward chaining*) com poda de hipóteses e escolha dinâmica de perguntas por maior alcance

---

## 1. Escopo do Domínio

| Item | Descrição |
|---|---|
| **Quem consulta** | Analista de crédito, gerente ou atendente de instituição financeira que faz a triagem de uma proposta de crédito pessoal. |
| **Decisão que o sistema apoia** | Qual encaminhamento de proteção dar à proposta: negar por risco de endividamento em Bets, bloquear preventivamente, enviar a um analista, ofertar limite protegido com alerta ou encaminhar a um programa de reeducação e tratamento de dívidas. |
| **Propósito de bem** | Evitar que crédito seja ofertado de forma irresponsável a pessoas já endividadas ou vulneráveis por conta do consumo em plataformas de apostas, e agir **antes** da negativação sempre que possível. |
| **O que fica de fora** | Cálculo do score, preço e taxas do crédito, garantias, prazos, antifraude e prevenção à lavagem de dinheiro, diagnóstico de transtorno de jogo (o sistema trata apostas apenas como **indicador de risco financeiro**) e a decisão final de alçada. |
| **Natureza do conhecimento** | Regras simplificadas para fins didáticos, inspiradas em práticas de crédito responsável e em dados públicos. Não substituem a política de crédito de uma instituição. |

---

## 2. Justificativa Social: Dados Públicos do Serasa

Dados consultados em 10/11/2026. Os números de inadimplência são do **Mapa da Inadimplência e Renegociação de Dívidas** da Serasa. Os números sobre apostas vêm de uma pesquisa da Serasa com o Instituto Opinion Box, conforme reportada pela imprensa (links na seção 12).

### 2.1 O cenário da inadimplência (Mapa da Inadimplência, setembro/2026)

| Indicador | Valor |
|---|---|
| Brasileiros com nome negativado | **84,2 milhões**, o maior número da série histórica, após 20 meses consecutivos de alta |
| Parcela da população adulta | **51,1%** |
| Crescimento | +6% em 12 meses (set/2025 a set/2026) e +34,17% desde 2020 |
| Dívidas em atraso | **R$ 597,4 bilhões** |
| Dívida média por negativado | **R$ 7.093,83**, cerca de 4,4 salários mínimos |
| Bancos e cartões | **27,16%** do total devido, a maior fatia |
| Financeiras | 20,66%, em segundo lugar pela primeira vez |
| Referência anterior | 81,7 milhões em fevereiro/2026, então um recorde |

> **Cuidado ao interpretar:** o indicador mede **pessoas com restrição no nome**, não famílias endividadas, e **não separa quanto da inadimplência vem de apostas**.

### 2.2 A relação entre apostas e endividamento (pesquisa Serasa e Opinion Box)

Pesquisa com **4.463 consumidores inadimplentes**, entrevistados de 12 a 18 de outubro de 2024, margem de erro de 1,4 ponto percentual.

| Achado | Resultado |
|---|---|
| Inadimplentes que já apostaram ao menos uma vez | **46%** |
| Desses, os que apostaram para tentar quitar dívidas | **44%** |
| Inadimplentes que já deixaram de pagar contas para apostar | **13%** |
| Endividados que apostaram e **não estavam inadimplentes antes** de apostar | **57%** |
| Apostadores endividados que usam o próprio salário para apostar | 69% |
| Endividados que perderam mais do que ganharam | 52% |
| Endividados que continuam apostando | 16% |
| Inadimplentes que chegaram a solicitar crédito para apostar | 10% (divulgado por um único veículo; confirme no relatório da Serasa) |

> **Nota:** as reportagens divergem em alguns percentuais (por exemplo, a parcela que continua apostando). Antes de citar um número na apresentação, confira o *Guia Serasa de Bets e Apostas Online* e o relatório original.

### 2.3 Evidência complementar (não é da Serasa)

Um estudo do Ibevar com a FIA Business School, citado pela economista-chefe da Serasa Experian, analisou o período de dezembro/2011 a dezembro/2025 e concluiu que as apostas passaram a pesar mais na inadimplência do que o crédito e os juros. Os coeficientes estimados foram **0,2255 para apostas**, contra 0,0440 para crédito sobre renda e 0,0709 para juros ao consumidor. Trata-se de associação estatística, não de prova de causa.

### 2.4 Como esses dados moldaram o sistema

| Evidência | Decisão de projeto |
|---|---|
| 44% apostam para quitar dívidas, 13% deixam de pagar contas e 10% pedem crédito para apostar | Quem **já tem restrição e mostra sinais de apostas** não deve receber novo crédito (**R1**): nova dívida para pagar dívida agrava o problema. |
| 57% não eram inadimplentes antes de apostar | O fato `historico_transacoes_apostas` é **independente** da restrição cadastral. É preciso agir antes da negativação (**R3**, **R4** e **R5**). |
| Bancos e cartões concentram 27% do total devido | O risco recai diretamente sobre quem concede crédito: a triagem responsável protege o consumidor e a instituição. |
| Restrição sem sinais de apostas | O caminho é tratar a dívida e reeducar, não apenas negar (**R2**). |

---

## 3. Mudança de Paradigma: de Processar Dados a Inferir e Decidir

Um programa procedural de crédito lê score, restrição e extrato, aplica `if/else` encadeados e imprime um resultado, com ordem das perguntas, lógica e dados misturados no mesmo código.

| Aspecto | Programa procedural (processamento de dados) | Este sistema especialista (inferência) |
|---|---|---|
| **Onde está o conhecimento** | Dentro do fluxo de `if/else` | Em dados declarativos (`BaseConhecimento`), separados do controle |
| **Quem decide a ordem das perguntas** | O programador, fixa | O motor, dinamicamente, pelo **maior alcance** |
| **Perguntas desnecessárias** | Feitas sempre | Evitadas por poda e curto-circuito |
| **Dado desconhecido (`?`)** | Costuma virar "não" ou gerar erro | Terceiro valor: a regra fica **bloqueada** e nada é afirmado sem prova |
| **Conclusões** | Só as programadas, na ordem codificada | **Deduzidas** a partir do estado de cada regra (confirmada, refutada, bloqueada ou pendente) |
| **Explicação** | Nenhuma | Rastro de justificativa: por que cada pergunta foi feita e cada regra aceita ou descartada |
| **Mudança de regra ou domínio** | Reescrever o código | Alterar só a base de conhecimento; o motor não muda |

### O que o motor deduz sozinho

1. **Estado das regras:** calculado sobre a memória de trabalho, sem perguntar nada.
2. **Poda:** um fato falso elimina a regra e as premissas restantes dela. Se a restrição é `n`, **R1** e **R2** caem de uma vez.
3. **Pergunta dirigida:** o próximo fato é o que aparece em mais regras ainda vivas (empate: ordem da base). Restrição e apostas aparecem em 5 regras cada; o score, em apenas 2.
4. **Reaproveitamento:** fatos respondidos ficam na memória e servem a qualquer hipótese seguinte.
5. **Dispensa de dados:** na ausência de restrição e de sinais de apostas, o motor conclui **R5** sem nunca perguntar o score.

---

## 4. Os 3 Fatos Observáveis

Cada fato é respondido com `s`, `n` ou `?`.

| # | Fato | Pergunta feita ao usuário | `s` (sim) | `n` (não) | `?` (não informado) |
|---|---|---|---|---|---|
| F1 | `score_credito_bom` | O score de crédito está acima da faixa de corte de risco? | Acima da faixa de corte | Abaixo da faixa de corte | Score não consultado |
| F2 | `possui_restricao_cadastral` | O cliente possui restrições ativas no CPF (Serasa e demais bureaus)? | Há restrição ativa | Nada consta | Consulta não realizada |
| F3 | `historico_transacoes_apostas` | Há indícios ou histórico recente de comprometimento de renda com transferências ou gastos em sites de apostas (Bets)? | Há indícios (ex.: transferências recorrentes a casas de apostas no extrato) | Nenhum indício | Extrato ou dados indisponíveis |

**Tratamento da ausência de dados:** `?` não equivale a "não". Um fato desconhecido **bloqueia** as regras que dependem dele, e o sistema informa que faltam dados em vez de negar ou conceder crédito sem base.

---

## 5. Base de Conhecimento: 5 Regras SE-ENTÃO

| Regra | SE (premissas) | ENTÃO (decisão) | Fundamento (prevenção ao superendividamento) |
|---|---|---|---|
| **R1** | `possui_restricao_cadastral = s` **E** `historico_transacoes_apostas = s` | **Negação Automática por Risco de Endividamento em Bets** | Nova dívida sobre cliente já negativado e com sinais de apostas agrava o ciclo (44% apostam para quitar dívidas; 13% deixam de pagar contas). Lei 14.181/2021 (CDC art. 54-D): avaliação responsável antes da oferta de crédito. |
| **R2** | `possui_restricao_cadastral = s` **E** `historico_transacoes_apostas = n` | **Programa de Reeducação e Tratamento de Dívidas** | Restrição sem apostas pede renegociação e educação financeira, não nova concessão. Lei 14.181/2021: prevenção e tratamento do superendividamento. |
| **R3** | `score_credito_bom = n` **E** `possui_restricao_cadastral = n` **E** `historico_transacoes_apostas = s` | **Bloqueio Preventivo de Crédito** | Perfil frágil com sinais de apostas, ainda sem restrição: bloqueia-se **antes da negativação** (57% não eram inadimplentes antes de apostar). |
| **R4** | `score_credito_bom = s` **E** `possui_restricao_cadastral = n` **E** `historico_transacoes_apostas = s` | **Análise Humana de Sobrevivência Financeira** | Bom score não elimina risco comportamental: um analista avalia se gastos essenciais estão preservados antes de qualquer oferta. |
| **R5** | `possui_restricao_cadastral = n` **E** `historico_transacoes_apostas = n` | **Oferecimento de Limite Protegido com Alerta** | Sem restrição e sem sinais de apostas, concede-se crédito com teto conservador e alertas de comprometimento de renda. |

### 5.1 Cobertura das 8 combinações

| Score | Restrição | Apostas | Regra | Decisão |
|---|---|---|---|---|
| s | s | s | R1 | Negação por risco de Bets |
| n | s | s | R1 | Negação por risco de Bets |
| s | s | n | R2 | Reeducação e tratamento de dívidas |
| n | s | n | R2 | Reeducação e tratamento de dívidas |
| s | n | s | R4 | Análise humana de sobrevivência financeira |
| n | n | s | R3 | Bloqueio preventivo |
| s | n | n | R5 | Limite protegido com alerta |
| n | n | n | R5 | Limite protegido com alerta |

As regras são **mutuamente exclusivas e exaustivas**: cada combinação de respostas conhecidas aciona exatamente uma regra (verificado por código). O score só é decisivo quando há sinais de apostas sem restrição (R3 e R4). Essa é uma simplificação didática: um banco real também usaria o score para precificar o limite.

> **Nota sobre as fontes legais:** Lei 14.181/2021 (superendividamento) e CDC art. 54-D são referências conceituais. Valide-as com o material da disciplina antes de citá-las formalmente.

---

## 6. Arquitetura

```
┌───────────────────┐   perguntas / respostas   ┌────────────────────┐
│ InterfaceConsole  │◄─────────────────────────►│ MotorInferencia    │
│ ou Interface GUI  │      callback obter_fato  │ (dedução e poda)   │
└───────────────────┘                           └─────┬────────┬─────┘
                                                      │        │
                                      lê regras/fatos │        │ lê/grava fatos
                                                      ▼        ▼
                                           ┌────────────────┐ ┌────────────────┐
                                           │ Base de        │ │ Memória de     │
                                           │ Conhecimento   │ │ Trabalho       │
                                           └────────────────┘ └────────────────┘
```

| Componente | Responsabilidade | O que **não** faz |
|---|---|---|
| `BaseConhecimento` | Declara fatos, decisões e regras como dados. | Não contém lógica de controle. |
| `MemoriaTrabalho` | Guarda respostas (`True`, `False`, `None`) da sessão. | Não decide nada. |
| `MotorInferencia` | Deduz o estado das regras, poda hipóteses, escolhe perguntas e gera o rastro. | Não imprime, não lê do teclado e não conhece regras de crédito. |
| `InterfaceConsole` e `interface_grafica.py` | Entrada de fatos, validação e exibição das justificativas. | Não tomam decisões. |

Trocar de domínio exige apenas trocar a `BaseConhecimento`: foi exatamente o que se fez nesta versão, sem alterar o motor.

---

## 7. Encadeamento para Trás (Goal-Driven)

No modo **1**, o usuário escolhe uma decisão como **hipótese**. O motor busca as regras que a concluem e:

1. Lê da memória as premissas já conhecidas.
2. Enquanto a regra estiver `PENDENTE`, escolhe o fato de maior alcance entre as premissas desconhecidas e pergunta.
3. A cada resposta reavalia: **premissa falsa** descarta a regra (curto-circuito), **desconhecida** a bloqueia e **todas verdadeiras** a confirmam.
4. Explica, premissa por premissa, o que foi verificado e o que se tornou desnecessário.

### 7.1 Simulação A: hipótese confirmada

**Objetivo:** *Negação Automática por Risco de Endividamento em Bets*. **Respostas, na ordem em que o motor perguntou:** F2 = `s`, F3 = `s`.

| Passo | Ação do motor | Pergunta e resposta | Resultado |
|---|---|---|---|
| 1 | Seleciona R1 (única regra que conclui o objetivo); memória vazia | n/a | Duas premissas a provar |
| 2 | Escolhe o fato de maior alcance: `possui_restricao_cadastral` (5 regras vivas; empate com apostas, desempate pela ordem da base) | F2, resposta `s` | Premissa 1 verdadeira; R3, R4 e R5 passam a refutadas |
| 3 | Resta `historico_transacoes_apostas` (2 regras vivas: R1 e R2) | F3, resposta `s` | Premissa 2 verdadeira |
| 4 | Todas as premissas de R1 verdadeiras | n/a | **R1 CONFIRMADA; hipótese CONFIRMADA** |

Saída real do sistema:

```text
HIPÓTESE: 'Negação Automática por Risco de Endividamento em Bets'
  Regra R1 concluiria a hipótese; premissas a provar:
    [pergunta] 'possui_restricao_cadastral' (aparece em 5 regra(s) viva(s)) -> resposta: sim.
    [pergunta] 'historico_transacoes_apostas' (aparece em 2 regra(s) viva(s)) -> resposta: sim.
  Verificação das premissas de R1:
    1. (possui_restricao_cadastral = sim): VERDADEIRA.
    2. (historico_transacoes_apostas = sim): VERDADEIRA.
    Todas verdadeiras -> R1 CONFIRMADA.
  => Hipótese CONFIRMADA.
CONCLUSÃO: Negação Automática por Risco de Endividamento em Bets -> CONFIRMADA pela regra R1.
Perguntas feitas nesta consulta: 2
```

### 7.2 Simulação B: poda e curto-circuito

**Objetivo:** *Negação Automática por Risco de Endividamento em Bets*. **Resposta:** F2 = `n`.

```text
HIPÓTESE: 'Negação Automática por Risco de Endividamento em Bets'
  Regra R1 concluiria a hipótese; premissas a provar:
    [pergunta] 'possui_restricao_cadastral' (aparece em 5 regra(s) viva(s)) -> resposta: não.
  Verificação das premissas de R1:
    1. (possui_restricao_cadastral = sim): FALSA (informado: não) -> regra descartada (curto-circuito).
    2. (historico_transacoes_apostas = sim): NÃO AVALIADA (desnecessária, regra já decidida).
  => Hipótese REFUTADA.
Perguntas feitas nesta consulta: 1
```

Sem restrição ativa, a negação por Bets não se aplica, e o sistema nem precisa olhar o extrato: **1 pergunta em vez de 2**.

### 7.3 Simulação C: dedução autônoma (modo 2)

Nenhuma decisão é escolhida pelo usuário: todas as regras são hipóteses simultâneas e o motor decide o que perguntar. **Respostas:** F2 = `n`, F3 = `s`, F1 = `n`.

```text
MODO AUTÔNOMO: todas as decisões são hipóteses; o motor poda regras e escolhe as perguntas.
  Estado: pendentes [R1, R2, R3, R4, R5] | descartadas [nenhuma] | bloqueadas por dado desconhecido [nenhuma]
  [pergunta] 'possui_restricao_cadastral' (aparece em 5 regra(s) viva(s)) -> resposta: não.
  Estado: pendentes [R3, R4, R5] | descartadas [R1, R2] | bloqueadas por dado desconhecido [nenhuma]
  [pergunta] 'historico_transacoes_apostas' (aparece em 3 regra(s) viva(s)) -> resposta: sim.
  Estado: pendentes [R3, R4] | descartadas [R1, R2, R5] | bloqueadas por dado desconhecido [nenhuma]
  [pergunta] 'score_credito_bom' (aparece em 2 regra(s) viva(s)) -> resposta: não.
  Estado: pendentes [nenhuma] | descartadas [R1, R2, R4, R5] | bloqueadas por dado desconhecido [nenhuma]
  => R3 confirmada: deduz-se 'Bloqueio Preventivo de Crédito'.
CONCLUSÃO: Bloqueio Preventivo de Crédito -> CONFIRMADA pela regra R3.
Perguntas feitas nesta consulta: 3
```

O score foi pedido por último e só porque ainda separava R3 de R4. Com F2 = `n` e F3 = `n`, o motor concluiria **R5 com 2 perguntas**, sem nunca perguntar o score. Com F2 = `?`, as cinco regras ficam bloqueadas e o sistema informa que nenhuma decisão pode ser deduzida.

### 7.4 Simulação D: reaproveitamento da memória

Depois da Simulação A (F2 = `s`, F3 = `s`), o usuário escolhe provar *Oferecimento de Limite Protegido com Alerta* (R5). O motor lê os dois fatos da memória, vê que ambos contradizem as premissas de R5 e refuta a hipótese com **0 novas perguntas**.

```text
HIPÓTESE: 'Oferecimento de Limite Protegido com Alerta'
  Regra R5 concluiria a hipótese; premissas a provar:
    [memória] 'possui_restricao_cadastral' já conhecido: sim (sem nova pergunta).
    [memória] 'historico_transacoes_apostas' já conhecido: sim (sem nova pergunta).
  Verificação das premissas de R5:
    1. (possui_restricao_cadastral = não): FALSA (informado: sim) -> regra descartada (curto-circuito).
    2. (historico_transacoes_apostas = não): FALSA (informado: sim) -> regra descartada (curto-circuito).
  => Hipótese REFUTADA.
Perguntas feitas nesta consulta: 0
```

---

## 8. Plano de Testes

Em todos os testes, a ordem das perguntas é a escolhida pelo motor: **F2 (restrição), F3 (apostas) e, só se necessário, F1 (score)**.

| # | Tipo | Modo e hipótese | Entradas (na ordem das perguntas) | Resultado esperado |
|---|---|---|---|---|
| T1 | Confirmação (R1), risco de Bets com restrição | 1: Negação por Bets | F2=`s`, F3=`s` | R1 confirmada; 2 perguntas |
| T2 | Confirmação (R2), restrição sem apostas | 1: Reeducação e Tratamento de Dívidas | F2=`s`, F3=`n` | R2 confirmada; 2 perguntas |
| T3 | Confirmação (R3), apostas e score baixo | 1: Bloqueio Preventivo | F2=`n`, F3=`s`, F1=`n` | R3 confirmada; 3 perguntas |
| T4 | Confirmação (R4), bom score com apostas | 1: Análise Humana | F2=`n`, F3=`s`, F1=`s` | R4 confirmada; 3 perguntas |
| T5 | Confirmação (R5), perfil limpo | 1: Limite Protegido | F2=`n`, F3=`n` | R5 confirmada; 2 perguntas; score não perguntado |
| T6 | Premissa falsa (curto-circuito) | 1: Negação por Bets | F2=`n` | Refutada; 1 pergunta; F3 "não avaliada" |
| T7 | Premissa falsa (curto-circuito) | 1: Bloqueio Preventivo | F2=`n`, F3=`n` | Refutada; 2 perguntas; F1 "não avaliada" |
| T8 | Negação: restrição sem apostas não é negação por Bets | 1: Negação por Bets | F2=`s`, F3=`n` | Refutada pela premissa 2; 2 perguntas |
| T9 | Premissa desconhecida (restrição) | 1: Negação por Bets | F2=`?` | Indeterminada; 1 pergunta |
| T10 | Premissa desconhecida (apostas) | 1: Negação por Bets | F2=`s`, F3=`?` | Indeterminada; 2 perguntas |
| T11 | Premissa desconhecida (score) | 1: Bloqueio Preventivo | F2=`n`, F3=`s`, F1=`?` | Indeterminada; 3 perguntas |
| T12 | Dedução autônoma com restrição e apostas | 2: autônomo | F2=`s`, F3=`s` | R1 deduzida; 2 perguntas; R3, R4 e R5 descartadas após a 1ª resposta |
| T13 | Dedução autônoma, bom score com apostas | 2: autônomo | F2=`n`, F3=`s`, F1=`s` | R4 deduzida; 3 perguntas |
| T14 | Dedução autônoma dispensando o score | 2: autônomo | F2=`n`, F3=`n` | R5 deduzida; 2 perguntas; score nunca perguntado |
| T15 | Dedução autônoma inconclusiva | 2: autônomo | F2=`?` | Nenhuma decisão deduzida; 1 pergunta; 5 regras bloqueadas |
| T16 | Reuso da memória | 1: Negação (T1), depois 1: Limite Protegido | F2=`s`, F3=`s`; depois escolher Limite Protegido | Segunda consulta com 0 perguntas; refutada |
| T17 | Entrada inválida | Qualquer | `talvez`, Enter vazio, depois `s` | Mensagem de erro e a pergunta se repete; nada inválido é gravado |
| T18 | Variações aceitas | Qualquer | `S`, `SIM`, `nao`, `não`, `ND` | Lidas como sim, sim, não, não e desconhecido |
| T19 | Opção de menu inválida | n/a | `9` no menu | "Opção inválida" e o menu volta |
| T20 | Nova consulta | Qualquer | Menu `4` e nova prova | Memória vazia; todas as perguntas refeitas |

---

## 9. Como Executar

```bash
python sistema_credito.py        # versão de console
python interface_grafica.py      # versão gráfica (Tkinter)
```

Os arquivos devem ficar na mesma pasta. No Linux, se faltar o Tkinter: `sudo apt install python3-tk`.

| Opção do menu (console) | Ação |
|---|---|
| `1` | Escolher uma decisão como hipótese e prová-la (encadeamento para trás) |
| `2` | Deixar o motor deduzir a recomendação, escolhendo as perguntas |
| `3` | Ver a memória de trabalho |
| `4` | Nova consulta (limpa a memória) |
| `0` | Sair |

A interface gráfica mostra a tabela das 5 regras com o estado deduzido em tempo real (verde confirmada, cinza refutada, amarelo bloqueada, azul pendente), a memória de trabalho, o rastro colorido e a conclusão. Quando o motor precisa de um fato, abre uma janela com Sim, Não e Não informado (atalhos `s`, `n` e `?`).

## 10. Estrutura do Repositório

```text
.
├── sistema_credito.py     # base de conhecimento, memória, motor e interface de console
├── interface_grafica.py   # interface gráfica (Tkinter) que reutiliza o motor
└── README.md              # esta documentação
```

---

## 11. Limitações e Considerações Éticas

- **Apostas como indicador de risco, não como diagnóstico.** O fato `historico_transacoes_apostas` sinaliza comprometimento de renda; o sistema não afirma nem avalia vício ou transtorno de jogo.
- **Origem e proteção dos dados.** Informações de extrato só devem ser usadas se obtidas de forma legítima e com consentimento (por exemplo, via Open Finance), em conformidade com a LGPD.
- **Decisão automatizada e revisão humana.** A negação automática (R1) deve poder ser contestada e revisada por uma pessoa (LGPD, art. 20). O rastro de justificativa do sistema existe justamente para tornar a decisão explicável. Valide a referência legal antes de citá-la.
- **Limites das estatísticas.** O Mapa da Inadimplência mede pessoas negativadas; a pesquisa sobre apostas ouviu inadimplentes e reflete autodeclaração de 2024. Nenhum dado aqui prova que apostas causam uma fração específica da inadimplência.
- **Simplificações do modelo.** Fatos binários (um sistema real usaria faixas e fatores de certeza) e uma única regra por decisão. O score só pesa quando há sinais de apostas sem restrição.
- **Extensões possíveis.** Encadeamento para frente, fatores de certeza para o fato de apostas e ordenação de perguntas por custo de consulta.

---

## 12. Fontes

- Serasa, *Mapa da Inadimplência e Negociação de Dívidas no Brasil* (setembro/2026): https://www.serasa.com.br/limpa-nome-online/blog/mapa-da-inadimplencia-e-renogociacao-de-dividas-no-brasil/
- Cobertura do Mapa de setembro/2026 (valor total, dívida média, composição por segmento): https://www.ocafezinho.com/2026-11-02/serasa-inadimplencia-bate-recorde-e-atinge-842-milhoes-de-brasileiros-em-setembro/
- Percentual da população adulta (51,1%): https://gazetamercantil.com/serasa-inadimplencia-84-milhoes-dividas-597-bilhoes
- Pesquisa Serasa e Opinion Box, 46%, 44%, 13%, amostra e margem de erro (InfoMoney, Estadão Conteúdo): https://www.infomoney.com.br/?p=2674784
- Pesquisa Serasa e Opinion Box, 57%, 69%, 52% e 16% (B3, Bora Investir): https://borainvestir.b3.com.br/noticias/57-dos-endividados-que-apostaram-em-bets-nao-eram-inadimplentes-antes-de-comecarem-a-apostar-revela-pesquisa-da-serasa/
- Pesquisa Serasa e Opinion Box, 10% que pediram crédito para apostar (Jornal Opção): https://www.jornalopcao.com.br/ultimas-noticias/serasa-aponta-como-o-crescimento-das-bets-afeta-a-saude-financeira-dos-brasileiros-658599/
- Estudo Ibevar e FIA Business School, citado pela economista-chefe da Serasa Experian (BB Investalk): https://investalk.bb.com.br/noticias/economia/bets-ja-sao-as-maiores-vilas-do-endividamento-no-brasil-mostra-estudo
- Guia Serasa de Bets e Apostas Online (material original da Serasa): consulte o site da Serasa para o documento completo.
