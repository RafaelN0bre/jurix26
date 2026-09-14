---
pdf:
  titulo: "CIF e LRC — Separação Modular da Análise Causal"
  subtitulo: "Documento de trabalho — anotador JURIX 2026"
  autor: "Rafael Nobre"
  data: "2026-09-07"
  saida: "docs/cif_lrc.pdf"
  remover: "andaime"
  referencias: "consolidar"
---

----------
REF -> Referência bibliográfica, deve ser colocada em ABNT, já, eu colocarei REF(nome) quando já souber, se não souber, você puxa

ORDER -> Uma instrução/seção a ser adicionada, pesquisa a ser feita

DOWNLOAD -> Busque pelo documento e salve em docs/papers, marque o ícone de check se já estiver

PDF -> gere com  /md2pdf docs/cif_lrc.md
       O bloco `pdf:` do frontmatter acima controla título, autor, saída e o que remover.
       remover: andaime | andaime+notas | nada      referencias: consolidar | inline
       Todo este bloco de legenda, os sufixos DOWNLOAD ✔/✖, os colchetes de nota
       operacional e o wrapper ORDER(...) somem no PDF. O conteúdo permanece.
------------

# CIF e LRC — a separação modular entre nexo fático e nexo juridicamente relevante

Documento de referência para a anotação. Descreve como Pisano, Prakken e Sartor (2026)
separam a análise causal em dois módulos de argumentação, expande o vocabulário de
predicados de cada um, cataloga as regras doutrinárias, e fixa os testes que o anotador usa
para decidir a que módulo cada premissa pertence.

REF: PISANO, Giuseppe; PRAKKEN, Henry; SARTOR, Giovanni. From cause-in-fact to legally relevant cause through argumentation. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 21., 2026, Singapura. Proceedings [...]. Nova York: ACM, 2026. 10 p. DOWNLOAD ✔ [`bib/Pisano2026_legal-relevant-cause.pdf`; paginação a confirmar na versão final dos anais]

REF: PISANO, Giuseppe; PRAKKEN, Henry; SARTOR, Giovanni; LIEPIŅA, Rūta. Modelling cause-in-fact in legal cases through defeasible argumentation. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 20., 2025. Proceedings [...]. Nova York: ACM Press, 2025. p. 278-287. DOWNLOAD ✔ [`bib/Pisano2025_cause-in-fact-aspic.pdf`]

REF: PRAKKEN, Henry; SARTOR, Giovanni. A formal framework for combining legal reasoning methods. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 19., 2023. Proceedings [...]. Nova York: ACM Press, 2023. p. 227-236. DOWNLOAD ✖ [é a base da arquitetura modular — prioridade de aquisição]

REF: MODGIL, Sanjay; PRAKKEN, Henry. The ASPIC+ framework for structured argumentation: a tutorial. Argument & Computation, v. 5, n. 1, p. 31-62, 2014. DOWNLOAD ✔

> **Nota sobre as referências desta seção.** Os dados bibliográficos de Prakken & Sartor
> (2023) e das fontes de Wright abaixo foram transcritos da lista de referências do próprio
> ICAIL 2026 e convertidos para ABNT. Não foram conferidos em fonte primária. Ver §9 para
> os casos em que a fonte apresenta erro aparente.

---

## 1. A separação: dois módulos, não duas seções de um mesmo sistema

O paper não separa CIF e LRC por conveniência expositiva. A separação é a **arquitetura de
argumentação modular** de Prakken & Sartor (2023), instanciada com dois módulos de
resolução de problemas conectados por uma *especificação de problema de metanível*.

Na arquitetura modular, cada módulo:

- tem sua **própria linguagem** lógica;
- tem sua **própria base de conhecimento** e seu próprio conjunto de regras;
- é avaliado **por conta própria**, podendo até usar um modelo de raciocínio diferente
  (o paper é explícito: um módulo pode ser argumentação derrotável, mas também dedução ou
  inferência bayesiana);
- **só se comunica com os outros por regras output-input**, cujos antecedentes são saídas de
  um ou mais módulos e cujo consequente é uma entrada de outro módulo.

Os dois módulos instanciados são:

**CIF — *cause-in-fact* (causalidade de fato, causalidade natural).** Recebe a teoria causal
`CT` do caso. Devolve a afirmação de que um fato é causa-de-fato de um efeito, segundo o
teste NESS. Corresponde exclusivamente ao **item (1)** dos cinco requisitos de
responsabilidade civil listados na introdução do paper.

**LRC — *legally relevant causation* (causalidade juridicamente relevante).** Recebe as
saídas do CIF como axiomas e decide, por regras doutrinárias derrotáveis, quais causas-de-fato
são juridicamente relevantes. Corresponde ao **item (2)**.

### 1.1. Os cinco requisitos, e onde os módulos ficam

O paper abre listando o que tipicamente deve estar presente para haver responsabilidade
civil. Reproduzo porque a lista é o mapa que impede o anotador de empurrar premissa para o
módulo errado:

| # | Requisito | Módulo |
|---|-----------|--------|
| (1) | o dano deve ter sido efetivamente causado por um ato ilícito | **CIF** |
| (2) | a causação deve ter se dado de modo ou em contexto que a torne relevante para o direito | **LRC** |
| (3) | o agente responsável deve estar em relação apropriada com o ato ilícito | *fora dos dois* |
| (4) | o agente deve ter agido com dolo ou culpa (salvo responsabilidade objetiva) | *fora dos dois* |
| (5) | não devem existir circunstâncias excludentes de responsabilidade (ex.: legítima defesa) | *fora dos dois* |

**Consequência prática imediata:** boa parte das premissas de um acórdão do STF — competência,
legitimidade, dever constitucional, configuração de culpa, responsabilidade objetiva do
art. 37, §6º, da CF — pertence aos itens (3), (4) e (5) e **não cabe em nenhum dos dois
módulos**. Forçá-las em CIF ou LRC corrompe os dois. Ver §7.3.

---

## 2. São *argumentation frameworks* diferentes?

Sim, e a diferença é mais funda do que "dois conjuntos de argumentos". Eles são **tipados
diferentemente** e **avaliados por maquinarias diferentes**.

| | **CIF** | **LRC** |
|---|---|---|
| Natureza | *família* de AFs + procedimento | **um** AF ASPIC+ padrão |
| Linguagem | fatos-token do mundo (`deFi`, `unFi`, `ig`, `de`) | predicados **sobre** relações causais (`caFa`, `leReCa`, `unexpected`, …) |
| Regras | regras causais (`r1: deFi ⇒ ig`) | regras doutrinárias (`cf2lrc`, `nwo`, `sc`, …) |
| Base de conhecimento | Def. 3.2: **`Kₙ = ∅`** — nada é axioma, tudo é derrotável | recebe `caFa` em **`Kₙ`** — indefectível |
| Avaliação | rotulação fundada em `AF_CT` **e** em cada `AF_CT+L` (expansão axiomática), comparadas | uma rotulação fundada, uma passada |
| Definições-chave | 3.1 explicação, 3.2 teoria causal, 3.3 expansão axiomática, 3.4 NESS, 3.5 but-for | eqs. (2) a (9) |
| Tipo de derrotabilidade | regra causal minada por fatos; contrafactual | *undercut* estratificado sobre regras nomeadas |
| Estabilidade | **neutro** quanto a jurisdição e doutrina | **doutrina-dependente e trocável** |
| Implementação (Arg2P) | solver externo, chamado via `prolog(...)`; Algoritmos 1 e 2 | teoria ASPIC+ comum, escrita à mão |

### 2.1. Por que o CIF não é "um" AF

A Definição 3.4 (NESS) exige, para dizer que φ é causa de ψ:

1. um argumento `D` na extensão fundada de `AF_CT` com conclusão φ;
2. um argumento `A` com conclusão ψ e uma **explicação** `E` para `A` (Def. 3.1 — o conjunto
   de argumentos do proponente em alguma estratégia vencedora mínima no jogo argumentativo
   fundado);
3. um conjunto de literais `L` com `−φ ∈ L`;
4. um argumento `B` **no framework expandido `AF_CT+L`** que ataque algum `C ∈ E` e esteja
   rotulado `in` ou `und` em `G(AF_CT+L)`.

Ou seja: a definição atravessa **dois frameworks distintos** e compara rótulos entre eles.
O CIF é o `AF_CT` original mais um `AF_CT+L` para cada intervenção considerada, mais o
procedimento que os confronta (Algoritmo 1). O LRC é um AF só.

### 2.2. A fronteira real: reificação

O que faz dos dois *frameworks* diferentes, e não um framework maior, é uma mudança de tipo:

- No **CIF**, a afirmação causal é uma **derivação** — uma estrutura de argumento construída
  por regras causais. Não há nenhum literal na linguagem do CIF que diga "φ causa ψ".
- No **LRC**, a mesma afirmação é um **termo**: `caFa(φ, ψ)`. É um literal sobre o qual se
  raciocina, que aparece como antecedente de regras, que pode ser argumento de outros
  predicados.

Essa reificação é a fronteira. Toda premissa que fala *sobre* uma relação causal já está do
lado de lá.

### 2.3. Três consequências estruturais

**(a) Nenhum argumento do CIF ataca argumento do LRC, e vice-versa.** A relação de ataque
não atravessa a fronteira. O único canal é a regra-ponte.

**(b) Dentro do LRC não se pode negar o nexo fático.** `caFa` entra em `Kₙ` — axiomas. Não é
premissa ordinária, logo não é *underminable*. Em todos os casos do paper (Kingston, Watson,
R v Jordan, Berry, Yania) a resposta do CIF permanece "sim, causou"; o que as defesas fazem é
bloquear a *inferência* `caFa ⇒ leReCa`.

> **Regra de anotação que decorre disso.** Nunca registre uma defesa jurídica como negação
> do nexo fático. "Houve rompimento do nexo causal" quase nunca significa, no formalismo,
> `¬caFa`; significa `¬cf2lrc`. São coisas formalmente incomparáveis.

**(c) A ponte não é de mão única nem de uma chamada só.** O predicado `butFor(χ, ψ)` é
antecedente da regra `SuCa` (eq. 5), no LRC, mas é **produzido** pelo CIF (Def. 3.5 /
Algoritmo 2). O paper diz explicitamente que a avaliação da relevância legal "pode envolver
novas chamadas ao módulo de causalidade de fato". Além disso, `Playout` "pode ser definido em
um módulo adicional" e `CausesNormally` é "delegado a um módulo de causalidade de tipo".
**A arquitetura é aberta a N módulos, não fechada em 2.**

---

## 3. A ponte

A especificação de metanível conecta os módulos por uma única regra output-input (eq. 1):

```
oi(...) : φ é NESS cause de ψ relativamente a AF_CT  ⇒  caFa(φ, ψ) ∈ Kₙ(LRC)
```

Na implementação em Arg2P (Listing 3) ela aparece como **regra estrita** (`->`, não `=>`) —
coerente com o fato de a saída entrar em `Kₙ`:

```prolog
oi(Y,Z) : check(Y,Z), prolog( causality::ness(X,Y,Z) ) -> caFa(Y,Z).
```

Dois detalhes que importam para a anotação:

- **`check(Y,Z)` é controle, não conhecimento.** São fatos fornecidos pelo usuário que
  declaram *quais pares causa-efeito devem ser verificados*. Sem `check`, a ponte não
  dispara. No vocabulário do protocolo, `check(Y,Z)` é exatamente a **causa candidata**.
- **`X` fica livre.** É a variável de intervenção, atribuída pelo solver. O anotador não a
  fornece.

Teoria integrada completa do caso Kingston, na notação do Arg2P (Listing 4), para referência:

```prolog
% ---------- Módulo Cause-in-Fact ----------
r0 : ig => de.
r1 : deFi => ig.
r2 : unFi => ig.
f1 :=> deFi.
f2 :=> unFi.

% ---------- Módulo Legally Relevant Causation ----------
cf2lrc(Y,Z) : caFa(Y,Z) => leReCa(Y,Z).
nwo(Y,Z,X)  : caFa(X,Z), caFa(Y,Z), prolog(X \= Y), -tortious(X) => -cf2lrc(Y,Z).
f :=> -tortious(unFi).

% ---------- Módulo Ponte ----------
oi(Y,Z) : check(Y,Z), prolog( causality::ness(X,Y,Z) ) -> caFa(Y,Z).
c1 : -> check(deFi, de).
c2 : -> check(unFi, de).
```

---

## 4. Serviços do módulo CIF

O CIF não exporta literais; exporta **respostas a consultas**. São três, mais duas noções
internas.

| Serviço | Definição | Consulta em Arg2P | Aridade | O que devolve |
|---|---|---|---|---|
| **NESS** | Def. 3.4 | `causality::ness(X, Cause, Effect)` | 3 (X livre) | φ é elemento necessário de um conjunto suficiente para ψ |
| **But-for** | Def. 3.5 | `causality::but_for(Cause, Effect)` | 2 | ψ deixa de ser justificado em `G(AF_CT+{−φ})` |
| **Expansão axiomática** | Def. 3.3 | interno | — | `CT + L = (AS, K ∪ L)`; análogo à *intervention* de Halpern & Pearl |
| **Explicação** | Def. 3.1 | interno | — | conjunto dos argumentos do proponente em estratégia vencedora mínima |
| **Teoria causal** | Def. 3.2 | entrada | — | `(AS, Kₙ ∪ Kₚ)` com `Kₙ = ∅` |

### 4.1. NESS e but-for não coincidem

Este é o ponto que o anotador mais erra. Em **sobredeterminação** (dois processos causais
independentemente suficientes), cada causa é NESS mas **nenhuma é but-for**.

- *Fairchild v Glenhaven* (2002): três exposições a amianto, duas bastam. Cada `Exᵢ` é causa
  NESS de `Di`; **nenhuma** é but-for, pois retirar uma isolada não impede a morte.
- *Kingston* (1927): dois incêndios, cada um suficiente. `deFi` e `unFi` são ambos NESS;
  `causality::but_for(deFi, de)` e `causality::but_for(unFi, de)` avaliam **false**.

**Consequência estrutural, e não trivial:** a regra `SuCa` (eq. 5) exige `butFor(χ, ψ)`.
Logo, **em casos de sobredeterminação a defesa de causa superveniente nunca dispara** — não
há causa but-for para ocupar o lugar de χ. `NWO` e `SC` são, nesses casos, mutuamente
excludentes. Se a anotação de um caso invoca as duas defesas ao mesmo tempo, há erro em
algum lugar.

---

## 5. Expansão dos predicados

O corpo do vocabulário está no LRC. O CIF não tem vocabulário fixo: seus átomos são os fatos
do caso (`deFi`, `unFi`, `Ex1`, `Ca`, `Di`, `Ga`, `Ma`, `PlSp`, `TrFa`, `YaHe`, `BiDi`…),
criados caso a caso.

### 5.1. Sortes (tipos de argumento) da linguagem do LRC

Antes da tabela, é preciso ver que o LRC manipula **três sortes distintas**, e confundi-las é
fonte de erro de anotação:

| Sorte | O que é | Exemplos no paper |
|---|---|---|
| **fato/evento** | átomo-token do caso, o mesmo do CIF | `deFi`, `unFi`, `Ma`, `Ga`, `PlSp`, `TrFa`, `¬YaHe` |
| **relação causal** | par ordenado (causa, efeito), reificado | o argumento de `caFa`, `leReCa`, `butFor` |
| **risco** | tipo de risco criado pela conduta — **não existe no CIF** | `SpCo` (riscos do excesso de velocidade) em *Berry* |

A sorte "risco" só aparece em `foreseeableRisk` e `playout`. Ela **não tem contrapartida no
módulo CIF**: não é um evento que ocorreu, é uma classe de desdobramentos possíveis. Por isso
o paper diz que `Playout` "pode ser definido em um módulo adicional".

### 5.2. Catálogo de predicados

Legenda da coluna **Origem**: `PONTE` = vem do CIF pela regra-ponte, entra como axioma;
`CIF` = é saída do CIF mas consumida como antecedente no LRC; `ANOT` = premissa que o
anotador extrai do acórdão; `DERIV` = derivado por regra interna do LRC; `MOD` = delegado a
um módulo ulterior.

| Predicado | Aridade e sortes | Origem | Significado | Onde aparece | Correspondente jurídico (BR) |
|---|---|---|---|---|---|
| `caFa(φ, ψ)` | 2 — (fato, fato) | **PONTE** | φ é causa-de-fato de ψ | eqs. 1-5; Kₙ(LRC) | nexo causal fático, causalidade natural |
| `leReCa(φ, ψ)` | 2 — (fato, fato) | **DERIV** | φ é causa juridicamente relevante de ψ | eqs. 2, 9 | nexo causal juridicamente relevante |
| `butFor(χ, ψ)` | 2 — (fato, fato) | **CIF** | sem χ, ψ não teria ocorrido | eq. 5 (antecedente de `SuCa`) | *conditio sine qua non* |
| `tortious(χ)` | 1 — (fato) | **ANOT** | χ é conduta/condição ilícita | eq. 3, negado | ilicitude do fato concorrente |
| `unexpected(χ)` | 1 — (fato) | **ANOT** | χ é altamente inesperado, extraordinário | eq. 5 | imprevisibilidade, caráter extraordinário |
| `after(χ, φ)` | 2 — (fato, fato) | **ANOT** | χ ocorreu depois de φ | eq. 5 | superveniência |
| `supersedingCause(χ, φ, ψ)` | **3** — (fato, fato, fato) | **DERIV** | χ é causa superveniente que desloca φ quanto a ψ | eqs. 4, 5 | causa superveniente relativamente independente; *actus novus interveniens*; fato de terceiro |
| `foreseeable(φ, ψ)` | 2 — (fato, fato) | **ANOT** | ψ era previsível a partir de φ | eq. 6, negado | previsibilidade *ex ante* |
| `foreseeableRisk(φ, χ)` | 2 — (fato, **risco**) | **ANOT** | χ é risco previsível criado por φ, e é o que torna φ ilícito | eq. 7 | risco criado pela conduta |
| `playout(χ, ψ)` | 2 — (**risco**, fato) | **MOD** | ψ é a realização/desdobramento do risco χ | eq. 7 | âmbito de proteção da norma; realização do risco |
| `om(φ)` | 1 — (fato) | **ANOT** | φ é uma omissão | eq. 8 | conduta omissiva |
| `obl(−φ)` | 1 — (fato) | **ANOT** | a ação omitida era juridicamente obrigatória | eq. 8, negado | dever jurídico de agir |
| `causesNormally(φ, ψ)` | 2 — (fato, fato) | **MOD** | ψ é consequência normal ou provável de φ | eq. 9 | causalidade adequada |
| `increasesProbability(φ, ψ)` | 2 — (fato, fato) | **MOD** | φ aumenta *ex ante* a probabilidade de ψ | §6, variante de eq. 9 | teoria do incremento do risco |
| `χ ≠ φ` | 2 | built-in | distinção de termos; `prolog(X \= Y)` | eqs. 3, 5 | — |
| `check(φ, ψ)` | 2 — (fato, fato) | **ANOT** | par causa-efeito submetido à verificação | Listing 3 | **causa candidata** |

### 5.3. Nomes de regra são literais

Mecanismo do ASPIC+ (função `n` da Def. 2.1; *undercut* da Def. 2.5): o nome de uma regra
derrotável **é um literal da linguagem**. Portanto estes também são predicados do LRC:

| Literal | Aridade | Papel |
|---|---|---|
| `cf2lrc(φ, ψ)` | 2 | nome da regra-presunção; `¬cf2lrc(φ,ψ)` é a conclusão de toda defesa |
| `noFor(φ, ψ)` | 2 | nome da defesa de imprevisibilidade; `¬noFor(φ,ψ)` é a conclusão de `RPL` |

É isso que permite a estratificação de §6.3: uma defesa ataca a presunção atacando o *nome*
da regra, e uma contra-defesa ataca a defesa atacando o *nome* da defesa.

### 5.4. Predicados discutidos mas não formalizados

O paper discute e deixa em aberto:

- **Enobrecimento (*ennoblement*).** O caso do sargento cruel: "atire no prisioneiro, se não
  atirar eu mesmo atiro". Tanto φ quanto `−φ` levam ao mesmo efeito. O paper diz preferir
  **aceitar a causalidade de fato e negar a relevância jurídica**, mas **não apresenta
  equação**.

  ORDER(formalizar a regra de enobrecimento como defesa LRC — a forma sugerida pelo paper é uma condição do tipo `caFa(φ,ψ), caFa(−φ,ψ) ⇒ ¬cf2lrc(φ,ψ)`, possivelmente modulada pela probabilidade do desfecho na alternativa não implementada; verificar como o ICAIL 2025 trata o caso, pois lá o enobrecimento é tratado dentro do CIF)

- **Graus de responsabilidade.** Chockler & Halpern transformam causalidade em noção
  gradual. O paper registra que isso é relevante para *graus* de responsabilidade, mas não
  para decidir *se* uma causa é juridicamente relevante — que é o foco. Fica fora.

---

## 6. Expansão das regras doutrinárias

### 6.1. Catálogo completo

| # | Regra | Forma | Tipo de ataque | Alvo | Doutrina | Caso |
|---|---|---|---|---|---|---|
| (2) | `cf2lrc(φ,ψ)` | `caFa(φ,ψ) ⇒ leReCa(φ,ψ)` | — (presunção) | — | Wright | base de todos |
| (3) | `NWO(φ,ψ,χ)` | `caFa(χ,ψ), χ≠φ, ¬tortious(χ) ⇒ ¬cf2lrc(φ,ψ)` | **undercut** | (2) | Wright — *no-worse-off* | *Kingston* |
| (4) | `SC(φ,ψ,χ)` | `supersedingCause(χ,φ,ψ) ⇒ ¬cf2lrc(φ,ψ)` | **undercut** | (2) | Wright — *superseding cause* | *Watson*; *R v Jordan* |
| (5) | `SuCa(φ,ψ,χ)` | `caFa(φ,ψ), caFa(χ,ψ), χ≠φ, after(χ,φ), unexpected(χ), butFor(χ,ψ) ⇒ supersedingCause(χ,φ,ψ)` | — (caracterização) | alimenta (4) | Wright | *Watson* |
| (6) | `NoFor(φ,ψ)` | `¬foreseeable(φ,ψ) ⇒ ¬cf2lrc(φ,ψ)` | **undercut** | (2) | previsibilidade | *Berry* |
| (7) | `RPL(φ,ψ)` | `foreseeableRisk(φ,χ), playout(χ,ψ) ⇒ ¬noFor(φ,ψ)` | **undercut** | **(6)** | Wright — *risk playout limitation* | *Berry* |
| (8) | `UnOm(φ,ψ)` | `om(φ), ¬obl(−φ) ⇒ ¬cf2lrc(φ,ψ)` | **undercut** | (2) | omissão | *Yania v. Bigan* |
| (9) | `cf2lrcBis(φ,ψ)` | `caFa(φ,ψ), causesNormally(φ,ψ) ⇒ leReCa(φ,ψ)` | — (**substitui** (2)) | — | causalidade adequada | direito penal italiano |
| (9′) | variante | `caFa(φ,ψ), increasesProbability(φ,ψ) ⇒ leReCa(φ,ψ)` | — (**substitui** (2)) | — | *law and economics* | ex.: envio por trem vs. rodovia |

REF: WRIGHT, Richard W. The NESS account of natural causation: a response to criticisms. In: GOLDBERG, Richard (Ed.). Perspectives on causation. Oxford: Hart Publishing, 2011. cap. 14. DOWNLOAD ✖

REF: WRIGHT, Richard W. The grounds and extent of legal responsibility. San Diego Law Review, v. 40, p. 1425-1532, 2003. DOWNLOAD ✖

REF: WRIGHT, Richard W. Causation and legal responsibility. CTLA Forum, 2025-2026. Disponível em: https://www.academia.edu/127567497/Causation_and_Legal_Responsibility. DOWNLOAD ✖ [é a fonte doutrinária central das eqs. 3-7 — prioridade de aquisição; ver a nota de erratas em §9]

REF: WRIGHT, Richard W.; PUPPE, Ingeborg. Causation: linguistic, philosophical, legal and economic. Chicago-Kent Law Review, v. 91, p. 461, 2016. DOWNLOAD ✖ [panorama das doutrinas alternativas de relevância]

REF: LANDES, William M.; POSNER, Richard A. The economic structure of intellectual property law. Cambridge: Belknap Press, 2003. DOWNLOAD ✖ [fonte da variante 9′]

### 6.2. Duas famílias de doutrina, e por que a distinção importa

O paper distingue expressamente dois modos de tornar a causalidade de fato juridicamente
relevante — e a escolha entre eles é **decisão de modelagem do artigo**, não dado do corpus:

**Família A — relevância presumida, restringida por defesas.** É a estrutura de Wright:
a regra (2) presume relevância, e as eqs. 3, 4, 6, 8 são exceções que a derrotam por
*undercut*. O ônus argumentativo recai sobre quem afasta a responsabilidade.

**Família B — relevância condicionada por requisitos positivos.** É a estrutura da eq. 9:
a relevância só se afirma se houver, *além* do nexo fático, causalidade adequada
(`causesNormally`) ou incremento de probabilidade (`increasesProbability`). O ônus recai
sobre quem afirma a responsabilidade.

> **Ponto de decisão para o artigo.** As duas famílias **não se somam**: a eq. 9 *substitui*
> a eq. 2, não convive com ela. Como a doutrina majoritária brasileira de responsabilidade
> civil adota a **teoria da causalidade adequada** (e não a *conditio sine qua non* pura),
> há um argumento forte de que a regra-base do corpus do STF seja a **eq. 9**, não a eq. 2 —
> o que muda toda a estrutura de ônus e todas as anotações de "razão da rejeição".
>
> ORDER(verificar, nos acórdãos do corpus, se o STF raciocina por presunção-com-defesas (família A) ou por requisito positivo de adequação (família B); a resposta define qual regra-base a formalização adota. Conferir também se o critério muda entre responsabilidade objetiva (art. 37, §6º, CF) e subjetiva)

### 6.3. Estratificação do LRC

O LRC é um sistema em camadas. Anotar sem enxergar as camadas produz premissas no nível
errado.

```
L0  caFa(φ,ψ)                            axioma vindo da ponte — inatacável no LRC
      │
L1    └─ cf2lrc ────────────► leReCa(φ,ψ)     presunção de relevância
             ▲
L2           ├── NWO      (¬tortious de causa paralela)
             ├── SC   ◄─── SuCa               [aux: caracteriza supersedingCause]
             ├── NoFor    (¬foreseeable)
             └── UnOm     (omissão sem dever de agir)
                  ▲
L3                └── RPL  (o dano é a realização de um risco previsível)
                           ataca NoFor, não cf2lrc
```

- **L2 ataca L1** concluindo `¬cf2lrc(φ,ψ)`.
- **L3 ataca L2** concluindo `¬noFor(φ,ψ)`. É exceção da exceção.
- **`SuCa` não ataca nada.** É regra de caracterização: produz o literal
  `supersedingCause(χ,φ,ψ)` que `SC` consome. Suas seis condições — nexo fático de ambas,
  distinção, posterioridade, imprevisibilidade e but-for — são os requisitos cumulativos da
  causa superveniente.

Isso importa diretamente para a anotação: no protocolo, "Razão da rejeição" (§5.3) e
"Argumentos da corrente vencedora enfrentados" (§5.5) costumam conter, misturados, premissas
de L2 e de L3. Um voto vencido que diz "mas o risco era exatamente esse" está em L3, não em
L2 — está atacando a *defesa*, não a *presunção*.

### 6.4. Os casos, um por um

| Caso | Nexo de fato | Defesa acionada | Premissas LRC | Resultado |
|---|---|---|---|---|
| **Kingston** (Wis. 1927) — incêndio do réu + incêndio de origem desconhecida, cada um suficiente | `caFa(deFi,de)` e `caFa(unFi,de)`; nenhum é but-for | `NWO` | `¬tortious(unFi)`, `deFi ≠ unFi` | réu não responde: causa paralela **não ilícita** |
| **Watson** (Ky. 1910) — vagão derrama gasolina, Duerr joga fósforo 3h depois | `caFa(Ga,In)`, `caFa(Ma,In)`; ambos but-for | `SC` via `SuCa` | `unexpected(Ma)`, `after(Ma,Ga)`, `butFor(Ma,In)` | ferrovia não responde: causa superveniente |
| **R v Jordan** (1956) — vítima esfaqueada morre por antibiótico a que era intolerante | `caFa(JoSt,ViDe)` | `SC` via `SuCa` | `unexpected(AdAn)`, `after(AdAn,JoSt)` | Jordan não responde: *actus novus* |
| **Berry v. Sugar Notch** (Pa. 1899) — autor em excesso de velocidade é atingido por árvore que cai | `caFa(PlSp,In)`, `caFa(TrFa,In)` | `NoFor`, **não** derrotada por `RPL` | `foreseeableRisk(PlSp,SpCo)`, `¬foreseeable(PlSp,In)`, `¬playout(SpCo,In)` | velocidade não é causa relevante: mera coincidência; sobra `TrFa` |
| **Yania v. Bigan** (Pa. 1959) — mineiro não socorre colega caído no poço | `caFa(¬YaHe,BiDi)` | `UnOm` | `om(¬YaHe)`, `¬obl(YaHe)` | não responde: sem dever de agir no direito norte-americano |
| **Cassazione Penale 12124/2023** — pais não dão tratamento de leucemia ao filho | causação por omissão | `UnOm` **não** se satisfaz | `om(φ)`, **`obl(−φ)`** | pais condenados: havia dever de cuidado |

*Berry* é o caso didático da estratificação: `NoFor` dispara porque o dano era imprevisível, e
`RPL` **não** consegue derrotá-la porque `¬playout(SpCo,In)` — ser atingido por árvore não é
realização de nenhum risco criado pelo excesso de velocidade. O par *Yania* / *Cassazione* é o
caso didático de que a **mesma regra** produz resultados opostos conforme o sistema jurídico
reconheça ou não o dever de agir.

### 6.5. Correspondentes no direito brasileiro

Hipóteses de mapeamento, para orientar a leitura dos acórdãos. **Não verificadas em fonte
primária** — ver a ordem ao final.

| Regra do paper | Dispositivo/doutrina BR candidato |
|---|---|
| `SC` + `SuCa` (eqs. 4-5) | **CP, art. 13, §1º** — "A superveniência de causa relativamente independente exclui a imputação quando, por si só, produziu o resultado; os fatos anteriores, entretanto, imputam-se a quem os praticou." A correspondência é quase literal: superveniência (`after`), independência relativa e suficiência própria (`butFor`). |
| `UnOm` (eq. 8) | **CP, art. 13, §2º** — "A omissão é penalmente relevante quando o omitente devia e podia agir para evitar o resultado", com as três fontes do dever (lei; assunção; ingerência). É o análogo direto do art. 40, *cpv.*, do CP italiano que o paper cita. |
| `NoFor` (eq. 6) | **CC, art. 393** — caso fortuito e força maior; e a exigência jurisprudencial de previsibilidade |
| `cf2lrcBis` (eq. 9) | **teoria da causalidade adequada**, majoritária na responsabilidade civil brasileira |
| `NWO` (eq. 3) | concausa preexistente ou concomitante não ilícita; fato da natureza |
| `playout` | **âmbito de proteção da norma**; teoria do risco criado |
| `¬tortious(χ)` | licitude do fato concorrente; fato exclusivo de terceiro **não** culposo |

> **Cuidado com "culpa exclusiva da vítima" e "fato de terceiro".** No vocabulário brasileiro
> essas expressões são tratadas como *excludentes do nexo causal*. No formalismo do paper
> elas quase nunca são `¬caFa`: são `¬cf2lrc`, via `SC` (se supervenientes e imprevisíveis)
> ou via `NWO` (se não ilícitas). Traduzir "exclui o nexo" por `¬caFa` é o erro de anotação
> mais custoso, porque destrói a estrutura em camadas.

ORDER(conferir em fonte primária a redação exata do art. 13, §§1º e 2º, do CP e do art. 393 do CC; levantar 2-3 acórdãos do STF do corpus que apliquem cada um dos correspondentes acima, para sustentar o mapeamento no artigo em vez de deixá-lo como analogia)

ORDER(pesquisar se há tratamento brasileiro consolidado para a limitação de *risk playout* — o âmbito de proteção da norma aparece mais na doutrina penal (imputação objetiva, Roxin) do que na civil; verificar se o STF usa o argumento e sob que nome)

---

## 7. Como classificar uma premissa

Quatro testes, do mais decisivo ao mais heurístico. Aplicar em ordem; o primeiro que der
resposta clara decide.

### 7.1. Os testes

**Teste 1 — intervenção.** Faz sentido perguntar "e se `¬p`?", e a resposta muda a
derivabilidade do efeito? Se apagar a premissa do mundo faz o dano **deixar de ocorrer** →
**CIF**. Premissas do CIF têm a forma "p ocorreu" / "p não ocorreu" (`Kₚ`) ou generalização
causal "p₁, p₂ ⇒ q" (`R`).

**Teste 2 — metanível.** Os lugares de argumento da premissa são *relações causais* ou *fatos
já qualificados juridicamente*? Se apagá-la do mundo **não** impede o dano, mas muda a
atribuição jurídica → **LRC**. `¬tortious(unFi)` não apaga o incêndio; `unexpected(Ma)` não
apaga a explosão.

**Teste 3 — troca de doutrina** (o mais afiado). Se você substituísse Wright pela
causalidade adequada, ou pelos critérios que o próprio STF usa, a premissa sobreviveria
intacta? **Sim → CIF. Seria reescrita ou descartada → LRC.**

Exemplo: "o INSS não fiscalizou a obra" sobrevive a qualquer doutrina de relevância — é CIF.
"A omissão de fiscalização é anormal e imprevisível" só existe dentro de uma doutrina
específica — é LRC.

**Teste 4 — vocabulário do acórdão.** Heurística de triagem, não critério.

| Marcadores de **CIF** | Marcadores de **LRC** |
|---|---|
| ocorreu, deu causa, produziu, contribuiu para | previsível / imprevisível |
| "sem X não teria acontecido" *(mas ver §7.2)* | normal / anormal, extraordinário |
| laudo, perícia, prova técnica | rompimento do nexo, causa superveniente |
| datas, sequência de eventos | fato de terceiro, culpa exclusiva da vítima |
| conteúdo do relatório | caso fortuito, força maior |
| | âmbito de proteção da norma |
| | risco criado, risco inerente |
| | dever de agir, concausa, adequação, proximidade |

### 7.2. Armadilhas

**"Se não fosse X, o dano não teria ocorrido" não é premissa.** É o teste but-for — um
**resultado** computado pelo CIF (Def. 3.5, Algoritmo 2). Anotar isso como premissa é o erro
mais comum. O que se anota são os fatos e as regras causais que o tornam verdadeiro.

**Classifique pelo lugar de produção, não pelo de consumo.** `butFor` é consumido no LRC
(eq. 5) e produzido no CIF. Nesse caso a premissa **não vai na `K` do LRC**: vira uma chamada
de ponte. O mesmo vale para qualquer `caFa`.

**Nunca anote `¬caFa` para uma defesa jurídica.** Ver §2.3(b).

**Não misture camadas.** Uma premissa que ataca uma defesa (L3) não é premissa da defesa (L2).
Ver §6.3.

**`NWO` e `SC` não coexistem em sobredeterminação.** Ver §4.1.

### 7.3. A terceira gaveta

Premissas que **não pertencem a nenhum dos dois módulos**:

- **Itens (3), (4) e (5)** dos requisitos de responsabilidade: imputação, culpa/dolo,
  excludentes. Num corpus de STF isso é volumoso.
- **Premissas normativas que escolhem a doutrina.** "Aplica-se responsabilidade objetiva"
  não é premissa *dentro* do LRC — é o que decide se a formalização usa `cf2lrc` (eq. 2) ou
  `cf2lrcBis` (eq. 9). É **seletor de módulo**, um nível acima.
- **Premissas processuais**: repercussão geral, conhecimento do recurso, modulação de efeitos.

O paper sinaliza essa ambiguidade explicitamente no caso da omissão (§6): a obrigação de agir
pode ser modelada **ou** como requisito de ilicitude (fora da análise causal, item 4) **ou**
como condição de relevância legal (dentro do LRC, item 2). São modelagens diferentes com
consequências diferentes. A escolha precisa ser registrada, não improvisada por anotador.

ORDER(decidir e documentar, para o corpus, se o dever de agir do art. 13, §2º, do CP e o dever constitucional de proteção entram como `¬obl(−φ)` no LRC ou como requisito de ilicitude fora dos módulos — e garantir que todos os anotadores sigam a mesma escolha, sob pena de os dossiês ficarem incomparáveis)

---

## 8. Mapeamento com o `protocol.md`

O protocolo já embute a distinção. O encaixe é quase exato:

| Campo do protocolo | Destino no formalismo |
|---|---|
| Fatos relevantes invocados / considerados (§5.1-5.3) | **CIF** — `Kₚ` |
| Relações causais afirmadas / consideradas | **CIF** — `R` (regras causais) |
| **Causas candidatas** afirmadas / consideradas | os pares `check(Y,Z)` submetidos à ponte |
| **Causas juridicamente relevantes** afirmadas / reconhecidas | conclusão `leReCa(φ,ψ)` do LRC |
| Causas juridicamente relevantes contestadas / rejeitadas | `¬cf2lrc(φ,ψ)` derivado por alguma defesa |
| **Razões da rejeição** (§5.3) | a mina de premissas LRC — é daqui que saem `NWO`, `SC`, `NoFor`, `UnOm` |
| Ponto de divergência / Razão da divergência (§5.5) | precisa registrar **em qual módulo e em qual camada** a divergência vive |
| Questões não decididas | tipicamente premissas `und` — nem `in` nem `out` |

### 8.1. Consequência de design: "causas candidatas rejeitadas" é ambíguo

O campo **"Causas candidatas rejeitadas"** (§5.3 e §5.6 do protocolo) funde duas rejeições
formalmente incomparáveis:

- rejeição **no CIF**: não houve nexo fático — o par nem passa no teste NESS;
- rejeição **no LRC**: houve nexo fático, mas foi afastada a relevância jurídica —
  `caFa(φ,ψ)` vale e `¬cf2lrc(φ,ψ)` também.

Hoje a diferença só apareceria em "Razões da rejeição", em texto livre, e depende de o
anotador tê-la percebido. Para o engenheiro de conhecimento, as duas rejeições geram
artefatos completamente diferentes: a primeira não gera nada no LRC; a segunda gera uma
instância de defesa, com suas premissas, sua camada e seu caso-modelo.

ORDER(avaliar acrescentar ao formulário um discriminador de nível de rejeição — "nexo fático" vs. "relevância jurídica" — e, no segundo caso, um seletor da defesa invocada (NWO / SC / NoFor / UnOm / outra). Isso tornaria a "Razão da rejeição" estruturada em vez de texto livre, sem aumentar a carga do jurista. Verificar impacto em `backend/models.py` e no `build_dossier`)

### 8.2. Divergência entre anotadores tem tipo

O modelo é de anotação múltipla cega. Duas divergências com o mesmo texto podem ter naturezas
opostas:

- divergência **CIF**: os anotadores discordam sobre um fato (`Kₚ`) ou sobre a regra causal
  (`R`). Resolve-se por prova, perícia ou releitura do acórdão.
- divergência **LRC**: os anotadores concordam sobre os fatos e discordam sobre a
  qualificação (`unexpected`, `foreseeable`, `tortious`). Resolve-se por argumento jurídico —
  ou não se resolve, e é exatamente o dado interessante para o artigo.
- divergência de **camada**: um anota como defesa (L2), outro como contra-defesa (L3).
  É erro de modelagem, não desacordo substantivo.

ORDER(considerar tipar o registro de divergência por módulo e camada; a divergência LRC entre anotadores é potencialmente o achado empírico do artigo — mede desacordo doutrinário genuíno, não ruído de anotação)

---

## 9. Erratas e inconsistências do texto-fonte

Registradas para não se propagarem na formalização.

> **Grafia de `foreseeable`.** O paper alterna entre `Foreseeable` (eq. 7,
> `ForeseeableRisk`) e `Forseeable` (eq. 6 e base de premissas do caso *Berry*). É o mesmo
> predicado, com erro de digitação. **Padronizar como `foreseeable`.**

> **Nome da regra na eq. 8.** A regra de omissão conclui `¬CF LRC(φ,ψ)` na eq. 8 e
> `¬CFLRC(¬YaHe,BiDi)` no exemplo de *Yania*, enquanto todas as demais defesas concluem
> `¬CF2LRC`. Trata-se do mesmo literal, faltando o "2". **Padronizar como `cf2lrc`.**

> **Átomos do caso *Watson*.** Os átomos declarados são `Ga` (derramamento), `Ma` (fósforo) e
> `Ig` (ignição dos vapores), com `r0 : Ga, Ma ⇒ Ig`. Mas a base de conhecimento do módulo
> LRC fala de `caFa(Ga, In)`, `caFa(Ma, In)`, `butFor(Ga, In)` — com `In` (*injury*), que não
> foi declarado nem aparece em `R`. Falta uma regra `Ig ⇒ In`. Ao reconstruir o caso,
> acrescentá-la.

> **Data da referência [30].** A lista de referências do paper traz "R. W. Wright.
> **2025-2006**. Causation and Legal Responsibility. In CTLA Forum **2025-2026**". O primeiro
> par de anos é evidentemente erro de digitação de "2025-2026". A referência ABNT em §6.1
> adota 2025-2026. **Conferir na fonte** ao citar — é a fonte doutrinária central das
> eqs. 3-7.

> **Título da Listing 1.** Está rotulada "No-Worse-Off Exception in the CIF Module", mas seu
> conteúdo é a teoria causal do caso *Kingston* (regras `r0`-`r2` e fatos `f1`-`f2`), sem
> nenhuma exceção. O rótulo foi copiado da Listing 2. O conteúdo está correto.

---

## 10. Resumo operacional

Para uso durante a anotação:

1. **O CIF não conhece direito.** Se a premissa menciona ilicitude, previsibilidade, dever,
   risco ou qualquer qualificação jurídica, ela não é do CIF.
2. **O LRC não conhece o mundo.** Ele só fala *sobre* relações causais que o CIF já
   estabeleceu. Ele nunca as nega.
3. **Toda defesa conclui `¬cf2lrc`, nunca `¬caFa`.**
4. **"Causa candidata" = `check(φ,ψ)`.** É o que se manda verificar, não o que se afirma.
5. **"Razão da rejeição" é onde moram as premissas do LRC.** É o campo mais denso do
   protocolo e o mais exigente.
6. **Se não couber em nenhum dos dois, é da terceira gaveta** — itens (3), (4) ou (5) da
   responsabilidade. Registre, não force.

---

## Anexo — inventário de aquisição

Já em `docs/papers/`:

```
ICAIL2026causation.pdf                     PISANO; PRAKKEN; SARTOR (2026)  — fonte deste documento
ICAIL2025causation.pdf                     PISANO; PRAKKEN; SARTOR; LIEPIŅA (2025) — módulo CIF
MODGIL_PRAKKEN_2014_ASPICplus_tutorial.pdf MODGIL; PRAKKEN (2014) — ASPIC+, undercut, n(r)
```

Pendentes, em ordem de prioridade:

```
PRAKKEN & SARTOR 2023  - A formal framework for combining legal reasoning methods (ICAIL, p. 227-236)
                         é a arquitetura modular inteira; sem ela o §1 fica sem base primária
WRIGHT 2025-2026       - Causation and Legal Responsibility (CTLA Forum; academia.edu)
                         fonte doutrinária das eqs. 3-7
WRIGHT 2003            - The Grounds and Extent of Legal Responsibility (San Diego L. Rev. 40, 1425-1532)
                         fonte dos casos Kingston, Watson, Berry
WRIGHT & PUPPE 2016    - Causation: linguistic, philosophical, legal and economic (Chi.-Kent L. Rev. 91, 461)
                         panorama de doutrinas alternativas — sustenta o §6.2
CALEGARI et al. 2022   - Arg2P (J. Logic and Computation 32(2), 369-401)  — implementação
HALPERN 2016           - Actual Causality (MIT Press) — contraponto Halpern-Pearl
HART & HONORÉ 1985     - Causation in the Law (OUP) — base do NESS
```

ORDER(baixar Prakken & Sartor 2023 e Wright 2025-2026 — são as duas lacunas que impedem citar o §1 e o §6 em fonte primária)
