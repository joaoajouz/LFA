# Ética e Impactos da Inteligência Artificial: Análise e Declaração de Uso de IA

**Projeto:** Sistema Especialista de Crédito Responsável (prevenção ao superendividamento por apostas online)
**Disciplina:** Inteligência Artificial e LFA, UDF Centro Universitário
**Professora:** Kadidja Valéria
**Atividade:** Aula de 17 de novembro de 2026
**Grupo 1:** João Pedro Figueiredo Ajouz

> Os trechos marcados como **[PREENCHER]** dependem de algo que só o autor pode afirmar: o argumento ouvido no debate em sala. Preencha-os e remova as marcações antes de entregar.

---

## 1. Leitura e vídeo

### 1.1 Artigo: questão de integridade acadêmica

*Lacerda Júnior, F. P. Uso ético da inteligência artificial generativa na educação superior: uma revisão integrativa (2023–2026). Revista Foco, v. 19, n. 8, ago. 2026.*

**Questão considerada: autoria e responsabilidade na declaração de uso de IA.** Parte relevante deste projeto (código, documentação e rascunhos) foi produzida com apoio de uma ferramenta de IA generativa. Declarar o uso exige dizer com precisão **o que a ferramenta fez**, **o que o autor aproveitou** e **como conferiu o resultado**, sem apresentar conteúdo gerado como se fosse integralmente autoral e sem atribuir à IA a responsabilidade pelas escolhas. A IA é uma ferramenta, e não integrante do grupo: a autoria e a responsabilidade são do estudante. Dados e referências sugeridos por uma ferramenta também precisam ser conferidos nas fontes originais, pois ela pode errar ou apresentar números imprecisos.

**Relação com o artigo:** o resumo do artigo observa que a difusão da IA generativa alterou as práticas de escrita, pesquisa, ensino e avaliação antes que muitas universidades definissem regras para seu uso, e o título propõe passar da proibição à governança. Nesse sentido, a declaração de uso de IA é um instrumento de governança: em vez de proibir ou omitir o uso, declaro com precisão o que a ferramenta fez e o que eu verifiquei.

### 1.2 Vídeo: trecho sobre impactos sociais ou responsabilidades institucionais

*Instituto de Estudos Avançados da USP. O Estado da Arte em Ética na Inteligência Artificial (jun. 2026), gravação de 2h01.*

- **Minutagem do trecho:** de **1:53:44 a 1:54:43** (resposta a uma pergunta do público sobre como traduzir a ética para a programação)
- **Ideia que levarei ao debate:** o palestrante (Steven Gouveia, organizador do livro apresentado no evento) defende que a ética precisa começar antes da própria ideia de um sistema e acompanhá-lo em três etapas: a concepção, o desenvolvimento e as consequências. Ele alerta que a tendência de achar que um código ético programado garante a ética do programa é equivocada, porque o código é condição necessária, mas não suficiente.
- **Relação com o projeto:** as cinco regras do sistema são o "código ético" da decisão e, sozinhas, não bastam. Por isso o projeto combina o propósito declarado (prevenir o superendividamento), a justificativa visível de cada saída, a possibilidade de corrigir dados, um responsável humano pela revisão e o acompanhamento das consequências (por exemplo, quantas negações são contestadas e revertidas).
- **Fonte:** Instituto de Estudos Avançados da USP, gravação disponível em https://youtu.be/x35_NJfXrpE

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
| Testes em pares: mudar um só fato e conferir que a decisão muda como previsto (o plano de testes do README prevê esses casos) | Plano |
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

**Posição do autor:** alternativa A, manter a negação automática, acompanhada das medidas de transparência e correção de dados descritas na seção 2.

### 3.2 Ideia do artigo ou do vídeo que sustenta a análise

**Ideia do artigo:** a passagem da proibição para a governança, isto é, em vez de proibir o uso da IA, estabelecer regras claras para usá-la com responsabilidade (Lacerda Júnior, 2026). **Aplicação ao dilema:** a mesma lógica vale para a decisão automática. Proibi-la por completo (alternativa B) ou aceitá-la sem regras seriam as duas pontas ruins; a governança, com regras explícitas, justificativa de cada decisão, possibilidade de corrigir dados e um responsável pela revisão, sustenta manter a negação automática da R1 (alternativa A) acompanhada dessas salvaguardas. **Ideia do vídeo (1:53:44 a 1:54:43):** a ética de um sistema não se esgota no código, que é necessário, mas não suficiente; por isso a regra automática só se justifica se vier acompanhada de escrutínio sobre o propósito, a justificativa de cada decisão e o acompanhamento das consequências.

### 3.3 Reflexão individual (após o debate)

Mantenho a negação automática da regra R1. Ela só dispara quando duas condições graves aparecem juntas, restrição ativa no CPF e indícios de comprometimento de renda com apostas, e os dados da Serasa que conferi mostram o risco de conceder novo crédito nesse perfil: entre os inadimplentes que apostaram, 44% o fizeram para tentar quitar dívidas. Nesse caso, esperar uma análise humana atrasaria a proteção e deixaria a decisão sujeita à pressão para aprovar. Reconheço o risco de falso positivo; por isso a negação não é silenciosa: ela vem com a justificativa das regras acionadas, e o cliente pode apresentar o dado corrigido para refazer a consulta. **[PREENCHER: argumento ouvido no debate que influenciou sua posição]** Para verificar se a medida funciona, eu acompanharia a proporção de negações de R1 que são contestadas e revertidas depois da correção dos dados: se for alta, a regra está negando por dado errado e precisa ser revista. Também testaria pares de casos que diferem só no indício de apostas, para confirmar que a decisão muda apenas como previsto.

---

## 4. Declaração de uso de sistemas de IA

### 4.1 IA incorporada ao projeto

O projeto utiliza um **sistema especialista baseado em regras de produção, com motor de inferência por encadeamento para trás (sem aprendizado de máquina)**, para **fazer a triagem de crédito responsável e prevenir o superendividamento ligado a apostas online**. O sistema recebe **três fatos sobre o cliente (score acima da faixa de corte, restrição ativa no CPF e indícios de comprometimento de renda com apostas), cada um respondido com sim, não ou não informado,** e gera **uma de cinco decisões de proteção (negação automática por risco de endividamento em apostas, bloqueio preventivo, análise humana, limite protegido com alerta ou programa de reeducação e tratamento de dívidas), acompanhada da justificativa do raciocínio**. Verifiquei seu funcionamento **executando o programa de console e testando a interface gráfica no meu computador; o README traz ainda um plano de 20 testes (confirmação de cada regra, curto-circuito, dado desconhecido, negação, reaproveitamento de memória e entradas inválidas) que serve de roteiro de verificação**. As limitações identificadas incluem: **fatos binários, sem graduação de risco; regras simplificadas para fins didáticos, não validadas por especialista em crédito; dependência de fontes externas para o score e para o dado de apostas, que podem estar desatualizados ou errados; o score só pesa nas regras R3 e R4; ausência de dados reais; e a negação automática (R1) exige revisão humana em um uso real**. A revisão cabe ao **analista de crédito ou gerente da instituição que utilizar o sistema; no âmbito acadêmico, a mim, como responsável pelo projeto**.

### 4.2 IA utilizada na elaboração do trabalho

Utilizei o **Claude, da Anthropic** (modelo **Claude Sonnet 5.5**) para **estruturar o domínio e as regras do sistema especialista, gerar o código em Python (versões de console e de interface gráfica), redigir e reorganizar o README, buscar e organizar dados públicos da Serasa, criar o fluxograma do motor de inferência e preparar rascunhos desta declaração**. Aproveitei **o código, a estrutura do README, as tabelas de regras e de testes, o fluxograma e partes do texto** após **executar o programa de console e testar a interface gráfica no meu computador e conferir nas fontes originais os números da Serasa usados no README**. As decisões de escopo (domínio de finanças, foco em apostas online e as orientações da professora sobre o motor de inferência e a ética) foram minhas. **Não utilizei outra ferramenta de IA.** A maior parte do código e do texto foi gerada pelo Claude a partir de instruções minhas; o Claude é uma ferramenta, e não integrante do grupo. Assumo a responsabilidade pelas escolhas, verificações e conteúdo da entrega.
