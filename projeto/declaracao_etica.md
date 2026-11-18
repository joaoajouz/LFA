# Ética e Impactos da Inteligência Artificial: Análise e Declaração de Uso de IA

**Projeto:** Sistema Especialista de Crédito Responsável (prevenção ao superendividamento por apostas online)
**Disciplina:** Inteligência Artificial e LFA, UDF Centro Universitário
**Professora:** Kadidja Valéria
**Atividade:** Aula de 17 de novembro de 2026
**Grupo 1:** João Pedro Figueiredo Ajouz

> Os trechos marcados como **[PREENCHER]** ou **[CONFIRMAR]** dependem de algo que só o autor pode afirmar (leitura do artigo, vídeo, debate em sala e o que ele de fato verificou). Revise e remova as marcações antes de entregar.

---

## 1. Leitura e vídeo

### 1.1 Artigo: questão de integridade acadêmica

*Lacerda Júnior, F. P. Uso ético da inteligência artificial generativa na educação superior: uma revisão integrativa (2023–2026). Revista Foco, v. 19, n. 8, ago. 2026.*

**Questão considerada: autoria e responsabilidade na declaração de uso de IA.** Parte relevante deste projeto (código, documentação e rascunhos) foi produzida com apoio de uma ferramenta de IA generativa. Declarar o uso exige dizer com precisão **o que a ferramenta fez**, **o que o autor aproveitou** e **como conferiu o resultado**, sem apresentar conteúdo gerado como se fosse integralmente autoral e sem atribuir à IA a responsabilidade pelas escolhas. A IA é uma ferramenta, e não integrante do grupo: a autoria e a responsabilidade são do estudante. Dados e referências sugeridos por uma ferramenta também precisam ser conferidos nas fontes originais, pois ela pode errar ou apresentar números imprecisos.

**[PREENCHER após ler o artigo]:** relacione essa questão a uma ideia do texto (o título, "Da proibição à governança", indica que o foco está em regras claras de uso, e não na proibição; confirme no artigo como ele trata a declaração de uso).

### 1.2 Vídeo: trecho sobre impactos sociais ou responsabilidades institucionais

*Instituto de Estudos Avançados da USP. O Estado da Arte em Ética na Inteligência Artificial (jun. 2026), gravação de 2h01.*

- **Minutagem do trecho:** **[PREENCHER: de hh:mm:ss a hh:mm:ss]**
- **Ideia que levarei ao debate:** **[PREENCHER: a ideia, em uma ou duas frases, e sua relação com o projeto]**

---

## 2. Análise ética do projeto

### 2.1 Apresentação do projeto

O Brasil vive um recorde de inadimplência e, segundo pesquisa da Serasa com a Opinion Box, muitos consumidores endividados recorreram a apostas online e boa parte deles não estava inadimplente antes de apostar. Para evitar que instituições financeiras ofertem crédito de forma irresponsável a pessoas já endividadas ou vulneráveis, desenvolvi, com apoio de IA, um **sistema especialista de triagem de crédito responsável**. Seus usuários são analistas de crédito ou gerentes, que respondem a três perguntas sobre o cliente (score acima da faixa de corte, restrição ativa no CPF e indícios de comprometimento de renda com apostas) com sim, não ou não informado. O sistema deduz uma de cinco decisões: negação automática por risco de endividamento em apostas, bloqueio preventivo, análise humana, limite protegido com alerta ou programa de reeducação e tratamento de dívidas. Podem ser afetados por suas saídas os **clientes** avaliados (que podem ter o crédito negado, bloqueado ou limitado), a **instituição** e **terceiros**, como familiares. A IA participa por meio de um **motor de inferência por encadeamento para trás** sobre regras de produção. **Todas as recomendações decorrem de cinco regras definidas por mim e redigidas com apoio de IA; não há modelo de aprendizado de máquina nem previsões geradas por modelo dentro do sistema.** O único elemento estatístico possível é o *score*, que entra como dado informado pelo usuário e é calculado fora do sistema, por um bureau de crédito.

### 2.2 Aspectos éticos

A coluna "No protótipo?" indica se a medida já existe no código entregue ou se é uma proposta para uma versão real.

#### Privacidade e dados

- **Situação concreta:** o fato `historico_transacoes_apostas` pressupõe acesso a extratos bancários, que revelam hábitos, saúde financeira e, indiretamente, comportamentos sensíveis. Um analista poderia consultar o extrato de um cliente sem necessidade ou sem consentimento.
- **Quem pode ser afetado:** os clientes avaliados e as pessoas com quem fazem transferências.
- **Medidas adotadas:**

| Medida | No protótipo? |
|---|---|
| O sistema não pede nome, CPF nem qualquer identificador: recebe apenas três respostas sim, não ou não informado | Sim |
| Nada é gravado em disco: a memória de trabalho existe apenas durante a sessão e é apagada em "Nova consulta" | Sim |
| Minimização: o motor pergunta só os fatos necessários para decidir; sem restrição e sem indício de apostas, o score nem é solicitado (regra R5) | Sim |
| Em uma versão real, o dado de apostas só seria obtido com consentimento expresso (por exemplo, via Open Finance) e para a finalidade declarada, conforme a LGPD | Proposta |

#### Viés e equidade

- **Situação concreta:** uma pessoa que aposta de forma eventual, com renda estável e sem dívidas, ou alguém cujas transferências a empresas de nome parecido foram confundidas com apostas, pode ser classificada com "indício de apostas" e receber análise humana ou bloqueio. O risco é maior para quem usa apostas como válvula de escape financeira e para grupos mais expostos a essas plataformas.
- **Quem pode ser afetado:** apostadores de baixo risco (falsos positivos) e grupos de menor renda, com maior chance de ter o perfil tratado como arriscado.
- **Medidas adotadas:**

| Medida | No protótipo? |
|---|---|
| As regras não usam idade, gênero, raça, local de residência ou renda; só os três fatos | Sim |
| O fato de apostas é definido como "comprometimento de renda", e não como "qualquer aposta", para não rotular apostadores comuns | Sim |
| Testes em pares: mudar um só fato e conferir que a decisão muda como previsto (os 20 casos do README cobrem essa verificação) | Sim |
| A única regra que decide sem pessoa (R1) é a de maior risco de dano; as demais encaminham, bloqueiam ou pedem análise humana | Parcial |
| Reconhecimento de limite: o *score* vem de um bureau e pode carregar vieses que eu não controlo | Declarado |

#### Transparência

- **Situação concreta:** um cliente é informado de que o crédito foi negado, sem saber por quê nem que a recomendação veio de um sistema automatizado.
- **Quem pode ser afetado:** o cliente, que não consegue entender nem contestar a decisão; e o analista, que poderia tomar a saída como decisão definitiva.
- **Medidas adotadas:**

| Medida | No protótipo? |
|---|---|
| Toda saída mostra a justificativa: qual regra foi acionada, quais premissas foram verdadeiras, falsas ou desconhecidas e quais nem precisaram ser avaliadas | Sim |
| A interface gráfica mostra o estado de cada regra e a memória de trabalho | Sim |
| Rotular a saída como "recomendação de sistema automatizado, sujeita à revisão humana" e informar o cliente do motivo em linguagem simples | Proposta |

#### Supervisão e responsabilidade

- **Situação concreta:** o cliente recebe uma negação por R1 porque a restrição no CPF já havia sido paga, mas o dado estava desatualizado.
- **Quem pode ser afetado:** o cliente negado indevidamente.
- **Medidas adotadas:**

| Medida | No protótipo? |
|---|---|
| A revisão cabe ao analista de crédito ou gerente da instituição, que decide; o sistema apenas recomenda | Declarado |
| O cliente pode apresentar o dado correto (por exemplo, a restrição quitada), o que permite refazer a consulta com os fatos atualizados | Sim |
| Em uma versão real, toda negação automática teria canal de contestação e revisão por pessoa, em linha com o direito de revisão de decisões automatizadas previsto na LGPD | Proposta |

#### Impacto social

- **Situação concreta:** o sistema protege um cliente em risco de superendividamento ao bloquear crédito antes da negativação. Se o indício de apostas estiver errado, ou se a recomendação for tratada como definitiva, uma pessoa com necessidade real de crédito fica sem acesso e pode recorrer a alternativas piores, como o crédito informal.
- **Quem se beneficia:** consumidores protegidos do ciclo de endividamento, famílias e a instituição, que reduz inadimplência.
- **Quem pode ser prejudicado:** clientes negados ou bloqueados por engano, e pessoas estigmatizadas por apostar.
- **Medidas adotadas:**

| Medida | No protótipo? |
|---|---|
| Quem tem restrição e não aposta é encaminhado a renegociação e reeducação financeira (R2), e não apenas negado | Sim |
| O bloqueio preventivo (R3) e a análise humana (R4) agem antes da negativação, sem excluir definitivamente | Sim |
| Tratar a saída sempre como sugestão e registrar os casos contestados para ajustar as regras | Proposta |

---

## 3. Debate em sala e reflexão individual

### 3.1 Dilema ético do projeto

**Dilema:** a regra R1 **nega automaticamente** o crédito a quem tem restrição ativa e indícios de apostas. Essa negação deve ser automática, ou toda negação por esse motivo deve passar por uma pessoa?

| | **Alternativa A: manter a negação automática** | **Alternativa B: exigir análise humana antes de negar** |
|---|---|---|
| **Vantagens** | Proteção imediata e em escala; decisão consistente e explicável pelo rastro de regras. | A pessoa pode ser ouvida e corrigir dados; reduz o dano de um falso positivo. |
| **Consequências negativas** | Cliente negado por dado errado ou desatualizado, sem ser ouvido; exclusão financeira e estigma; risco de a saída ser tratada como definitiva. | Mais lento e caro; o analista pode ser pressionado a aprovar, e decisões podem variar de pessoa para pessoa. |

### 3.2 Ideia do artigo ou do vídeo que sustenta a análise

**[PREENCHER:]** indique a ideia escolhida (do artigo ou do vídeo, com minutagem), explique em uma ou duas frases e conecte-a ao dilema acima, apontando se ela favorece a alternativa A, a B ou uma combinação.

### 3.3 Reflexão individual (após o debate)

*Parágrafo pessoal, escrito depois do debate em sala. Responda, com suas próprias palavras:*

1. **Qual decisão manteria ou mudaria?** (a negação automática de R1, a exigência de análise humana ou uma solução intermediária)
2. **Qual argumento ouvido no debate influenciou sua posição?**
3. **Como verificaria se a medida funciona?** (por exemplo, acompanhando quantas negações são contestadas e quantas revertidas, ou testando casos com a mesma situação financeira e histórico de apostas diferente)

**[PREENCHER: parágrafo individual]**

---

## 4. Declaração de uso de sistemas de IA

### 4.1 IA incorporada ao projeto

O projeto utiliza um **sistema especialista baseado em regras de produção, com motor de inferência por encadeamento para trás (sem aprendizado de máquina)**, para **fazer a triagem de crédito responsável e prevenir o superendividamento ligado a apostas online**. O sistema recebe **três fatos sobre o cliente (score acima da faixa de corte, restrição ativa no CPF e indícios de comprometimento de renda com apostas), cada um respondido com sim, não ou não informado,** e gera **uma de cinco decisões de proteção (negação automática por risco de endividamento em apostas, bloqueio preventivo, análise humana, limite protegido com alerta ou programa de reeducação e tratamento de dívidas), acompanhada da justificativa do raciocínio**. Verifiquei seu funcionamento por meio de **um plano de 20 testes descrito no README (confirmação de cada regra, curto-circuito, dado desconhecido, negação, reaproveitamento de memória e entradas inválidas) e da execução do programa no meu computador [CONFIRMAR quais testes você executou]**. As limitações identificadas incluem: **fatos binários, sem graduação de risco; regras simplificadas para fins didáticos, não validadas por especialista em crédito; dependência de fontes externas para o score e para o dado de apostas, que podem estar desatualizados ou errados; o score só pesa nas regras R3 e R4; ausência de dados reais; e a negação automática (R1) exige revisão humana em um uso real**. A revisão cabe ao **analista de crédito ou gerente da instituição que utilizar o sistema; no âmbito acadêmico, a mim, como responsável pelo projeto**.

### 4.2 IA utilizada na elaboração do trabalho

Utilizei o **Claude, da Anthropic** (**[CONFIRMAR modelo e versão usados]**) para **estruturar o domínio e as regras do sistema especialista, gerar o código em Python (versões de console e de interface gráfica), redigir e reorganizar o README, buscar e organizar dados públicos da Serasa, criar o fluxograma do motor de inferência e preparar rascunhos desta declaração**. Aproveitei **o código, a estrutura do README, as tabelas de regras e de testes, o fluxograma e partes do texto** após **[DESCREVER como conferiu, corrigiu ou testou: por exemplo, executei o programa e os cenários de teste no meu computador; conferi o comportamento das regras contra a tabela do README; verifiquei os números da Serasa nas fontes originais; ajustei o texto à orientação da professora. Liste apenas o que de fato fez.]** **[Se usou outra ferramenta, como o NotebookLM, declare-a aqui, com a finalidade.]** A maior parte do código e do texto foi gerada pelo Claude a partir de instruções minhas; o Claude é uma ferramenta, e não integrante do grupo. Assumo a responsabilidade pelas escolhas, verificações e conteúdo da entrega.
