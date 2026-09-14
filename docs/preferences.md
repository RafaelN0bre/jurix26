---
pdf:
  titulo: "Critérios para Ponderação e Aplicação de Preferências"
  subtitulo: "Documento de trabalho — anotador JURIX 2026"
  autor: "Rafael Nobre"
  data: "2026-09-04"
  saida: "docs/preferences.pdf"
  remover: "andaime"
  referencias: "consolidar"
---

----------
REF -> Referência bibliográfica, deve ser colocada em ABNT, já, eu colocarei REF(nome) quando já souber, se não souber, você puxa

ORDER -> Uma instrução/seção a ser adicionada, pesquisa a ser feita

DOWNLOAD -> Busque pelo documento e salve em docs/papers, marque o ícone de check se já estiver

PDF -> gere com  /md2pdf docs/preferences.md
       O bloco `pdf:` do frontmatter acima controla título, autor, saída e o que remover.
       remover: andaime | andaime+notas | nada      referencias: consolidar | inline
       Todo este bloco de legenda, os sufixos DOWNLOAD ✔/✖, os colchetes de nota
       operacional e o wrapper ORDER(...) somem no PDF. O conteúdo permanece.
------------

# Definição geral de Critérios para ponderação e aplicação de preferências

Dado que a resolução de conflitos se dá prioritariamente em cima das preferências
(The ASPIC+ framework for structured argumentation: a tutorial)

REF: MODGIL, Sanjay; PRAKKEN, Henry. The ASPIC+ framework for structured argumentation: a tutorial. Argument & Computation, v. 5, n. 1, p. 31-62, 2014. DOWNLOAD ✔

Estamos definindo um critério de ponderação de critérios de ordenação para preferência, e estaremos avaliando algumas possibilidades.

São três os critérios avaliados — **acúmulo de argumentos**, **hierarquia normativa e institucional** e **pesos teleológicos** —, integrados ao final em uma única relação de preferência (ver §4).

---

## 1. Acúmulo de Argumentos

Acúmulo de Argumentos (Accrual): soma do peso probatório de múltiplos fatores fáticos independentes. Uma conclusão sustentada por várias premissas agrupadas (ex: falha estrutural + longo lapso temporal + omissão específica) pode somar força suficiente para derrotar uma regra contrária baseada em uma única premissa forte.

REF: PRAKKEN, Henry. A study of accrual of arguments, with applications to evidential reasoning. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 10., 2005, Bolonha. Proceedings [...]. Nova York: ACM Press, 2005. p. 85-94. DOWNLOAD ✔

REF: VERHEIJ, Bart. Accrual of arguments in defeasible argumentation. In: DUTCH/GERMAN WORKSHOP ON NONMONOTONIC REASONING, 2., 1995, Utrecht. Proceedings [...]. Delft: Delft University of Technology; Utrecht: Universiteit Utrecht, 1995. p. 217-224. DOWNLOAD ✔

REF: PRAKKEN, Henry. Modelling accrual of arguments in ASPIC+. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 17., 2019, Montreal. Proceedings [...]. Nova York: ACM, 2019. p. 103-112. DOWNLOAD ✔

REF: PRAKKEN, Henry. Argument accrual, ASPIC+ and bipolar argumentation frameworks. In: COMPUTATIONAL MODELS OF ARGUMENT (COMMA 2026). Amsterdã: IOS Press, 2026. (Frontiers in Artificial Intelligence and Applications). DOWNLOAD ✔ [paginação a confirmar]

> **NOTA DE CORREÇÃO — referência descartada.** A referência que circulava como
> "ROTH, Abraham; VERHEIJ, Bart; RESSLER, Wouter. The accrual of arguments in legal
> reasoning. ICAIL 2007, p. 287-288" **não existe**. O sumário completo do ICAIL 2007
> (46 entradas, via dblp) mostra que as páginas 287-288 são de PAGALLO, Ugo; RUFFO,
> Giancarlo — "P2P systems in legal networks: another small world case". Não há paper
> de accrual no ICAIL 2007 e não existe publicação conjunta desses três autores
> ("Wouter Ressler" não consta em nenhuma base). O que Bram Roth publicou no ICAIL 2007
> foi "Strategic argumentation: a game theoretical investigation" (p. 81-90), com
> Riveret, Rotolo e Governatori — outro tema.
> Substituída por VERHEIJ (1995), que é a fonte fundacional de accrual em argumentação
> jurídica e é citada como antecedente pelo próprio Prakken (2005). Note a coincidência
> das páginas 217-224 — provavelmente a origem da corrupção da citação.

### 1.1. Os três princípios de accrual (PRAKKEN, 2005, §3)

Qualquer tratamento satisfatório de acúmulo deve satisfazer:

1. **§3.1 — Acúmulos são às vezes *mais fracos* que seus elementos.** Razões podem
   ser interdependentes. Consequência literal do paper:
   *"the possibility of interacting reasons implies that in general the strength of an
   accrual cannot be calculated from the strengths of its elements."*
2. **§3.2 — O acúmulo torna seus elementos inaplicáveis.** Quando o acúmulo se aplica,
   as regras individuais que o compõem saem de cena, mesmo que o acúmulo acabe derrotado.
3. **§3.3 — Razões viciadas (*flawed*) não acumulam.** Se um elemento é derrotado por
   undercut ou por derrota de subargumento, ele é removido *antes* do acúmulo.

### 1.2. Restrição estrutural: undercut em ASPIC+ ignora preferências

Definição 3.12 do tutorial (MODGIL; PRAKKEN, 2014):

> *"A **defeats** B iff A **undercuts** or successfully rebuts or successfully undermines B."*

E o Exemplo 3.13, explícito:

> *"the undercutting attack of B₃ on A₂ (and thereby on A₃) succeeds as a defeat
> **irrespective of the argument ordering**."*

Apenas *rebuttal* e *undermining* passam pelo teste de preferência (`A ⊀ B'`). **Undercut
derrota sempre.** Portanto, atribuir peso a um undercutter é inócuo: nenhum acúmulo o
supera. Combinado com o §3.3 acima, um argumento undercutted sequer entra no acúmulo.

### 1.3. Proposta de ordem e pesos ORDER(proposta básica de ordem e pesos, com esses objetos: falha estrutural, lapso temporal, omissão específica)

**Decisão de modelagem prévia:** o lapso temporal **não** pode ser modelado como undercut
se quisermos que o acúmulo o dispute (§1.2). Modelamo-lo como *rebuttal* sobre a conclusão
intermediária `nexo_causal`.

*Proposta de Modelagem de Acúmulo:*

*   **r1:** `falha_estrutural ⇒ nexo_causal` — Peso: **leve**
*   **r2:** `omissão_específica_custódia ⇒ nexo_causal` — Peso: **médio**
*   **r3:** `lapso_temporal_longo ⇒ ¬nexo_causal` — Peso: **grave**
    (rebuttal sobre `nexo_causal`, **não** undercut da regra)

*   **Conflito isolado:** r3 (grave) derrota r2 (médio). O Estado vence pela quebra temporal.

*   **Regra de acúmulo explícita** (PRAKKEN, 2019) — estipulada, não somada:

    *   **r₁,₂:** `falha_estrutural ∧ omissão_específica ⇒ nexo_causal` — Peso: **grave+**

    *Justificativa do peso estipulado:* a conjunção descreve omissão estatal *continuada e
    conhecida*, qualitativamente distinta de qualquer dos fatores isolados — não é a soma
    deles. A responsabilidade do Estado se mantém.

*   Ao aplicar-se, **r₁,₂ torna r1 e r2 individualmente inaplicáveis** (PRAKKEN, 2005, §3.2).
*   Se r1 ou r2 for undercutted, ele **não entra** no acúmulo e r₁,₂ não se forma
    (PRAKKEN, 2005, §3.3).

> **Por que não `Peso(r1 ∪ r2) = 3 + 4 = 7`.** A soma aritmética é exatamente o que
> PRAKKEN (2005) existe para refutar (§3.1). No caso concreto, falha estrutural e omissão
> específica de custódia **não são independentes** — a omissão de custódia é em boa medida
> *consequência* da falha estrutural; somar contaria o mesmo fato duas vezes.
>
> **Ganho para o artigo:** o peso do accrual passa a ser um *dado anotado* — decisão
> jurídica explícita, rastreável até o acórdão — em vez de um artefato aritmético. Encaixa
> melhor no protocolo do anotador.

> **Checagem pendente.** O padrão fático (fuga + dano ~3 meses depois) parece ser o do
> **Tema 362 / RE 608880**, cuja tese fala em ausência de *"nexo causal direto entre o
> momento da fuga e a conduta praticada"*. Conferir a redação exata antes de citar: a
> formulação da tese decide se o lapso temporal é rebuttal do nexo ou undercut da
> imputação — e essa escolha determina se o acúmulo pode ou não prevalecer.

---

## 2. Hierarquia Normativa e Institucional

Hierarquia Normativa e Institucional: atribuição de pesos com base nos princípios clássicos de resolução de conflitos (Lex Superior, Lex Posterior, Lex Specialis) e na força vinculante do tribunal. Em modelagens brasileiras, teses de Repercussão Geral do STF recebem preferência estrutural máxima sobre entendimentos de instâncias inferiores ou regras gerais.

REF: PRAKKEN, Henry; SARTOR, Giovanni. A dialectical model of assessing conflicting arguments in legal reasoning. Artificial Intelligence and Law, v. 4, n. 3-4, p. 331-368, 1996. DOWNLOAD ✔

REF: MODGIL, Sanjay; PRAKKEN, Henry. A general account of argumentation with preferences. Artificial Intelligence, v. 195, p. 361-397, 2013. DOWNLOAD ✔

*Especificação dos Princípios como Metarregras de Preferência (≺):*

*   **Lex Superior (Hierarquia):** norma de grau superior derroga inferior. Se a premissa A vem de uma Tese de Repercussão Geral do STF e a premissa B de um tribunal local, A ≻ B.
*   **Lex Specialis (Especialidade):** norma específica prevalece sobre geral. A regra especial de Risco Anormal na custódia de presos sobrepõe-se à regra geral de omissão subjetiva.
*   **Lex Posterior (Cronologia):** norma mais recente revoga anterior de mesma hierarquia, servindo como desempate subsidiário.

---

## 3. Pesos Teleológicos

Pesos Teleológicos ou Principiológicos: a preferência é definida avaliando-se os valores, princípios constitucionais ou objetivos de políticas públicas subjacentes às regras em conflito (ex: o argumento fundado na proteção à integridade física recebe peso superior ao argumento fundado na reserva do possível).

*Bases de Ponderação e Hierarquia:*
A literatura resolve isso mapeando argumentos para valores subjacentes (Value-Based Argumentation Frameworks — VAFs) ou aplicando a fórmula de ponderação de Robert Alexy, onde a audiência define a preferência axiológica.

REF: BENCH-CAPON, Trevor J. M. Value-based argumentation frameworks. In: INTERNATIONAL WORKSHOP ON NON-MONOTONIC REASONING, 9., 2002, Toulouse. Proceedings [...]. 2002. p. 444-453. DOWNLOAD ✔
[o próprio Bench-Capon lista 444-453 em sua bibliografia; circula também como 443-454 — conferir]

REF: BENCH-CAPON, Trevor; SARTOR, Giovanni. A model of legal reasoning with cases incorporating theories and values. Artificial Intelligence, v. 150, n. 1-2, p. 97-143, 2003. DOWNLOAD ✔

REF: ALEXY, Robert. Teoria dos direitos fundamentais. Tradução de Virgílio Afonso da Silva. São Paulo: Malheiros, 2008. DOWNLOAD ✖
[livro sob direito autoral vigente, sem versão aberta legítima — não baixado.
 Corrigir a citação: a 1ª ed. brasileira é 2008; a 2ª ed. é 2011. Falta o tradutor.
 Para a formalização computacional da ponderação, usar SARTOR (2010) no lugar.]

### 3.1. Bases de ponderação de pesos teleológicos ORDER(procure por bases de pesos teleológicos, existe já alguma hierarquia para ponderação de pesos teleológicos. procure por referências)

**Resposta curta: não existe hierarquia substantiva universal de valores.** O que a
literatura oferece são quatro *mecanismos* distintos para produzir a ordenação. Escolher
qual usar é uma decisão do artigo, não um dado da literatura.

**(a) Ordenação relativa à audiência — VAF.** BENCH-CAPON (2002) não fixa hierarquia:
parametriza. Um VAF é `⟨AF, val: A → V, audiência⟩`, onde a audiência é uma ordenação sobre
V. Um ataque só derrota se o valor do atacado **não** for preferido ao do atacante.
Distingue argumentos *objetivamente* aceitáveis (em toda ordenação) dos *subjetivamente*
aceitáveis (em alguma). **Aplicação direta ao projeto:** anotadores divergentes = audiências
distintas; e a divergência entre votos vencedor/vencido do acórdão é literalmente um
conflito de ordenações de valores.

**(b) Ordenação extraída de precedentes.** BENCH-CAPON & SARTOR (2003): o `Vpref` da teoria
**não é estipulado, é derivado** — cada precedente em que o tribunal decidiu por um lado
apesar de valores conflitantes gera uma preferência de valores. **É a base mais defensável
para um artigo sobre acórdãos do STF**: a hierarquia sai do próprio corpus anotado, não da
opinião do anotador.

**(c) Escala formal de ponderação — Alexy.** Aqui **sim há uma hierarquia canônica**: a
**escala triádica** *leve / médio / grave*, mapeada geometricamente em **2⁰, 2¹, 2² = 1, 2, 4**.
Fórmula do Peso: `W_ij = (I_i · G_i · S_i) / (I_j · G_j · S_j)`, onde `I` = intensidade da
intervenção, `G` = peso abstrato e `S` = confiabilidade das premissas empíricas. Formalizada
para AI & Law em SARTOR (2010).

**(d) Pesos aprendidos empiricamente.** GRABMAIR & ASHLEY (2017), sistema VJAP: aprende
*quantitative value effect tradeoffs* a partir dos resultados dos casos, prevê desfechos e
justifica com argumentos. Estado da arte em pesos teleológicos empíricos.

**Fundacional.** BERMAN & HAFNER (1993) — *"the missing link"*: modelos de CBR precisam
representar os *propósitos* atrás das regras. Retomado em BENCH-CAPON (2002), *The Missing
Link Revisited*.

**E no direito brasileiro?** Há uma ordenação **doutrinária/jurisprudencial** consolidada,
útil como ponto de partida mas que precisa ser rotulada como tal (não é formal):
**dignidade da pessoa humana / mínimo existencial > vida e integridade física > direitos
prestacionais > interesses orçamentários (reserva do possível)**. O STF reiteradamente
rejeita a reserva do possível oposta ao mínimo existencial. Isso dá apoio interno ao exemplo
usado acima (integridade física ≻ reserva do possível), em vez de apoio apenas importado.

REF: BERMAN, Donald H.; HAFNER, Carole D. Representing teleological structure in case-based legal reasoning: the missing link. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 4., 1993, Amsterdam. Proceedings [...]. Nova York: ACM, 1993. p. 50-59. DOWNLOAD ✖ [ACM bloqueia download automático]

REF: BENCH-CAPON, Trevor J. M. The missing link revisited: the role of teleology in representing legal argument. Artificial Intelligence and Law, v. 10, n. 2-3, p. 79-94, 2002. DOWNLOAD ✔

REF: SARTOR, Giovanni. Doing justice to rights and values: teleological reasoning and proportionality. Artificial Intelligence and Law, v. 18, n. 2, p. 175-215, 2010. DOWNLOAD ✔

REF: ALEXY, Robert. On balancing and subsumption: a structural comparison. Ratio Juris, v. 16, n. 4, p. 433-449, 2003. DOWNLOAD ✖ [acesso fechado — verificado via OpenAlex]

REF: GRABMAIR, Matthias. Predicting trade secret case outcomes using argument schemes and learned quantitative value effect tradeoffs. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 16., 2017, Londres. Proceedings [...]. Nova York: ACM, 2017. p. 89-98. DOWNLOAD ✖ [acesso fechado]

REF: ATKINSON, Katie; BENCH-CAPON, Trevor. Value-based argumentation. Journal of Applied Logics, v. 8, n. 6, p. 1543-1588, 2021. DOWNLOAD ✔ [PDF é o número completo da revista; o artigo está em p. 1543-1588]

---

## 4. Proposta integrada de pesos ORDER(Descreva de maneira simples uma proposta de pesos)

**Princípio de projeto: não somar critérios de naturezas diferentes.** Hierarquia normativa
é sobre *autoridade da fonte*; peso teleológico é sobre *substância do valor*; accrual é
sobre *quantidade de suporte*. Colapsar os três num único número perde justamente a
informação que o artigo quer expor. Usa-se **ordem lexicográfica**.

### Proposta Integrada de Ponderação

Cada regra derrotável `r` recebe uma tripla anotada **⟨ h(r), v(r), a(r) ⟩**.

#### h(r) — Nível hierárquico da fonte (Lex Superior)

| h | Fonte |
|---|-------|
| 3 | CF/88, Súmula Vinculante, Tese de Repercussão Geral do STF |
| 2 | Lei federal, jurisprudência dominante do STJ |
| 1 | Jurisprudência de tribunal local |
| 0 | Doutrina, argumento não vinculante |

#### v(r) — Peso teleológico (escala triádica de Alexy)

| v | Grau | Exemplo no domínio |
|---|------|--------------------|
| 4 | grave | vida, integridade física do custodiado, dignidade |
| 2 | médio | segurança jurídica, limite da responsabilidade estatal |
| 1 | leve  | eficiência administrativa, reserva do possível |

#### a(r) — Fator de acúmulo

Definido apenas entre regras de **mesma conclusão**. Não é soma: é o peso estipulado da
regra de acúmulo explícita (§1.3).

#### Relação de preferência (lexicográfica)

```
r ≻ r'  sse   h(r) > h(r')
        ou    h(r) = h(r')  e  v(r) > v(r')
        ou    h(r) = h(r')  e  v(r) = v(r')  e  a(r) > a(r')
```

Desempates subsidiários, nesta ordem: **Lex Specialis**, depois **Lex Posterior**.

#### Por que lexicográfica e não soma ponderada

1. Evita somar grandezas incomensuráveis ("ser do STF" + "proteger a vida").
2. Torna a hierarquia normativa inderrotável por acúmulo de argumentos de instância
   inferior — que é como o sistema brasileiro de fato opera.
3. Cada nível é auditável em separado pelo anotador.

#### Exemplo aplicado ao caso da fuga

| | Argumento | h | v | Resultado |
|---|---|---|---|---|
| **A** | Tese de RG do STF: sem nexo causal direto, não há responsabilidade objetiva | **3** | 2 | **vence** |
| **B** | Risco anormal na custódia ⇒ dever de proteger integridade física | 2 | **4** | perde |

Pelo nível `h`, **A** vence — apesar de **B** ter peso teleológico superior. Esse é o
resultado juridicamente correto, e é precisamente o que a soma ponderada erraria
(B somaria 2+4 = 6 contra 3+2 = 5). Serve como caso de teste do critério.

#### Limite conhecido

A ordem lexicográfica é rígida: nenhum acúmulo de razões teleológicas vence uma diferença
hierárquica mínima. Onde isso for indesejado, restringir a comparação de `h` ao caso de
fontes de mesma natureza e deixar `v` decidir — ou usar EAFs (MODGIL, 2009), que permitem
argumentar sobre a própria ordenação de preferências em vez de fixá-la.

REF: MODGIL, Sanjay. Reasoning about preferences in argumentation frameworks. Artificial Intelligence, v. 173, n. 9-10, p. 901-934, 2009. DOWNLOAD ✖ [acesso fechado]

REF: MODGIL, Sanjay; PRAKKEN, Henry. Revisiting preferences and argumentation. In: INTERNATIONAL JOINT CONFERENCE ON ARTIFICIAL INTELLIGENCE, 22., 2011, Barcelona. Proceedings [...]. Menlo Park: AAAI Press/IJCAI, 2011. p. 1021-1026. DOWNLOAD ✔

---

## 5. Aplicação: onde as preferências entram no CIF e no LRC

Esta seção fecha a ligação entre a tripla ⟨h, v, a⟩ definida em §4 e a arquitetura modular
descrita em `docs/cif_lrc.md` e `docs/adjudicators.md`. Responde a três perguntas: **em que
etapa** a preferência é aplicada, **em qual módulo** ela vale, e **o que ela não alcança**.

REF: PRAKKEN, Henry. A formal model of adjudication dialogues. Artificial Intelligence and Law, v. 16, n. 4, p. 305-328, 2008. DOWNLOAD ✔ [`bib/Prakken2008-adjudication.pdf`; o PDF é o manuscrito aceito, sem volume nem paginação finais — dados a conferir]

### 5.1. Etapa: fase de decisão, e como último instrumento

No modelo de adjudicação de Prakken (2008), o argumento de prioridade é **exclusivo do
adjudicador e exclusivo da fase de decisão**. No exemplo integralmente formalizado (§5.2
daquele paper), toda prioridade é lance do juiz:

```
α24 [δ12]:  π11 > δ12  since convinced by π11
```

As partes movem `claim`, `why`, `concede`, `retract` e `argue` — nunca prioridade. E o
adjudicador, na fase de argumentação, só move `burden`, `illegal` e `terminate`.

Dentro da fase de decisão há ordem. As quatro decisões do adjudicador (§4.3 do paper) são,
nesta sequência:

| # | Decisão | Instrumento |
|---|---|---|
| 1 | a premissa não disputada se sustenta? | *premise-attack* |
| 2 | o argumento é **internamente válido**? | **undercut** |
| 3 | há razão para contra-argumento adicional? | novo argumento |
| 4 | o argumento é **dialeticamente válido**? | **argumento de prioridade** |

**A preferência é o quarto e último instrumento.** E entra num lugar sintático preciso: o
`since` do lance. A tripla ⟨h, v, a⟩ de §4 é o **conteúdo da razão da prioridade** — é o que
substitui o `convinced` do exemplo por um critério auditável.

> **Condição de disparo: a preferência é residual ao ônus da persuasão.** Prakken observa,
> ao discutir uma distribuição alternativa do ônus, que se o adjudicador avalia os argumentos
> como antes, então *"in the decision phase he does not have to move a priority argument
> against δ12, **since plaintiff is already winning this line of dispute**"*.
>
> Ou seja: `≺` só é invocada onde a alocação do ônus da persuasão **não decidiu a linha
> sozinha**. Antes de anotar uma preferência é preciso verificar se o ônus já bastava —
> preferência anotada onde o ônus resolvia é ruído, não dado.

### 5.2. Módulo: a tripla ⟨h, v, a⟩ é LRC-shaped

Os três componentes de §4 pressupõem que o conflito é **normativo**:

- `h` ordena por **autoridade da fonte jurídica**;
- `v` ordena por **valor constitucional**;
- `a` ordena por **acúmulo de razões jurídicas**.

Nenhum deles ordena conflito **probatório**. "Peso teleológico de um laudo pericial" não
significa nada; "hierarquia normativa de um depoimento" tampouco.

Mas o CIF precisa de ordenação — e ironicamente **o único argumento de prioridade concreto de
Prakken (2008) é probatório**: `α24: π11 > δ12 since convinced by π11` decide qual comparação
de assinaturas prevalece. É conflito de prova, não de norma. A tripla de §4 não o alcança.

> **Conclusão.** ⟨h, v, a⟩ é a ordenação do **LRC**. O **CIF** exige uma ordenação separada,
> de natureza epistêmica. É o que §5.3 propõe.

### 5.3. A ordenação do CIF, ancorada no `S` de Alexy

A saída já está neste documento, em §3.1(c). A Fórmula do Peso de Alexy é

```
W_ij = (I_i · G_i · S_i) / (I_j · G_j · S_j)
```

com `I` = intensidade da intervenção, `G` = peso abstrato e `S` = **confiabilidade das
premissas empíricas**. A fórmula **já se parte exatamente na linha CIF/LRC**:

| Fator | Módulo | Natureza |
|---|---|---|
| `I`, `G` | **LRC** | normativa — intensidade e peso abstrato |
| `S` | **CIF** | epistêmica — confiabilidade da prova |

Isto não é analogia: é a mesma distinção, já presente na formulação original de Alexy, entre
as premissas normativas da ponderação e a confiabilidade das premissas empíricas que a
sustentam.

#### s(r) — confiabilidade epistêmica

Proposta, mantendo a escala triádica de §4 por coerência:

| s | Grau | Fonte típica no acórdão |
|---|------|-------------------------|
| 4 | seguro | fato incontroverso, confissão, perícia não impugnada |
| 2 | plausível | prova testemunhal, indício convergente, generalização causal aceita |
| 1 | duvidoso | indício isolado, prova impugnada, generalização causal contestada |

#### Relação de preferência no CIF

```
r ≻_CIF r'   sse   s(r) > s(r')
```

**Sem pilha lexicográfica.** `h` e `v` não entram — e no caso de `h` há razão estrutural, não
apenas conceitual: em recurso extraordinário o STF **não reexamina prova** (Súmula 279), de
modo que a hierarquia da fonte não ordena achados de fato. A matéria fática chega fixada das
instâncias ordinárias.

[Súmula 279/STF — "Para simples reexame de prova não cabe recurso extraordinário". Redação
citada de memória; conferir em fonte primária antes de usar no artigo.]

ORDER(verificar a Súmula 279 do STF em fonte primária e checar se a limitação de reexame probatório de fato torna a ordenação do CIF ociosa no corpus — se o STF nunca ordena prova, s(r) pode ser irrelevante para acórdãos de RE e só valer para a reconstrução das instâncias de origem)

ORDER(decidir se s(r) deve compor multiplicativamente com v(r) à maneira da fórmula de Alexy, ou permanecer como ordenação separada por módulo; a fórmula original multiplica I·G·S, o que sugere composição, mas isso reintroduz a soma de grandezas incomensuráveis que §4 rejeita)

### 5.4. O que as preferências não alcançam

Cruzando §1.2 deste documento com as duas camadas de decisão de Prakken (2008), fecha-se um
resultado que os dois foram encontrar por caminhos independentes.

§1.2 estabeleceu, a partir de MODGIL & PRAKKEN (2014, Def. 3.12 e Ex. 3.13), que **undercut
derrota sempre, independentemente da ordenação de argumentos**. Prakken (2008) estabelece que
a decisão de **validade interna** do adjudicador se exprime **por undercut**. Logo:

> A decisão de validade interna é **imune à ordenação de preferências**. Só a decisão de
> validade dialética é território de `≺`.

| Camada de decisão | Instrumento | Preferência opera? |
|---|---|---|
| validade interna | undercut | **não** |
| validade dialética | prioridade | **sim** |

#### Consequência verificada no Caso 003

A formalização do CIF do Caso 003 (RE sobre responsabilidade do Estado por crime de foragido)
produziu um grafo em que **todos os ataques são undercuts** — nenhum *undermining*, nenhum
*rebutting*. Fuga, latrocínio, morte e danos são incontroversos em todas as cinco
perspectivas; o litígio inteiro recai sobre a regra `FugaPreso ⇒ Latrocinio`.

Pela tabela acima, isso significa que **no CIF daquele caso as preferências não operam em
nenhum ponto**. A ordenação só passa a ter função no LRC — que é, aliás, o que se espera de
um caso cuja divergência é doutrinária e não probatória.

É um teste útil do critério: se um caso anotado apresentar preferências relevantes no CIF, ou
o caso é genuinamente probatório, ou há erro de camada na anotação — provavelmente um
*rebuttal* anotado onde havia undercut.

### 5.5. Quem atribui os pesos

Vale a regra do `protocol.md` §2.5 — *a tradução para categorias formais pertence ao
engenheiro de conhecimento*:

| Quem | O que registra |
|---|---|
| **jurista** (Etapa 2, perspectivas de papel adjudicador) | "o Min. X entendeu que prevalece o argumento Y sobre Z, porque […]" + passagem vinculada |
| **engenheiro** (canonicalização) | converte em ⟨h, v, a⟩ / s e na relação `≺` |

A tripla é **artefato de canonicalização, não de anotação**. Pedir ao jurista que atribua
`v = 4` viola o princípio de autoria jurídica do protocolo e contamina a medida: a divergência
entre anotadores passa a se confundir com a divergência entre ministros.

#### Só `v` e `a` carregam sinal de divergência

| Componente | Varia por adjudicador? | De onde vem |
|---|---|---|
| `h` | **não** — objetiva dada a fonte | proveniência da regra; metadados |
| `v` | **sim** | fundamentação do voto |
| `a` | **sim** | estipulação da regra de acúmulo no voto |
| `s` | **sim** | avaliação da prova no voto |

Daí um diagnóstico automático: **se dois ministros divergem e `h` é igual entre os argumentos
em conflito, a divergência está necessariamente em `v`, `a` ou `s`** — a divergência D6 da
tipologia em `docs/adjudicators.md` §9.2, que é o conflito axiológico puro.

---

## 6. Critérios de preferências

- Especificidade do Dever Jurídico de Agir
- Intervenção Causal
- Autonomia do Evento Superveniente

## Anexo — Inventário de `docs/papers/`

Baixados nesta rodada (13 arquivos):

```
ATKINSON_BENCH-CAPON_2021_Value-based_argumentation_survey_JAL.pdf
BENCH-CAPON_2002_The_Missing_Link_Revisited_teleology_AILaw.pdf
BENCH-CAPON_2002_Value_Based_Argumentation_Frameworks_NMR.pdf
BENCH-CAPON_SARTOR_2003_Model_legal_reasoning_theories_values_AIJ.pdf
MODGIL_PRAKKEN_2011_Revisiting_Preferences_and_Argumentation_IJCAI.pdf
MODGIL_PRAKKEN_2013_General_account_argumentation_with_preferences_AIJ_corrected2018.pdf
MODGIL_PRAKKEN_2014_ASPICplus_tutorial.pdf
PRAKKEN_2005_accrual_ICAIL.pdf
PRAKKEN_2019_Modelling_accrual_in_ASPICplus_ICAIL.pdf
PRAKKEN_2026_Argument_accrual_ASPICplus_bipolar_COMMA.pdf
PRAKKEN_SARTOR_1996_dialectical_model_AILaw.pdf
SARTOR_2010_Doing_justice_to_rights_and_values_proportionality_AILaw.pdf
VERHEIJ_1995_Accrual_of_arguments_in_defeasible_argumentation.pdf
```

Pendentes (acesso fechado ou bloqueado — exigem acesso institucional):

```
ALEXY 2008  - Teoria dos Direitos Fundamentais (livro, direito autoral vigente)
ALEXY 2003  - On Balancing and Subsumption (Ratio Juris, closed access)
BERMAN & HAFNER 1993 - ICAIL (gold OA na ACM DL, mas download automático bloqueado)
GRABMAIR 2017 - ICAIL (closed access)
MODGIL 2009 - Reasoning about preferences in AFs (AIJ, closed access)
PRAKKEN & SARTOR 2007 - Formalising arguments about the burden of persuasion (ICAIL, p. 97-106)
                        permite ao adjudicador argumentar sobre o ônus em vez de recebê-lo
                        dado; companheiro natural de §5.1
```

Acrescentado depois desta rodada, e do qual §5 depende:

```
2008_Prakken_FormalModel_AILaw.pdf   PRAKKEN (2008) — diálogos de adjudicação;
                                     fonte de §5.1 e §5.4
```
