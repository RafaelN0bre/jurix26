---
pdf:
  titulo: "Adjudicadores — Votos como Decisão sobre o AF das Partes"
  subtitulo: "Documento de trabalho — anotador JURIX 2026"
  autor: "Rafael Nobre"
  data: "2026-09-07"
  saida: "docs/adjudicators.pdf"
  remover: "andaime"
  referencias: "consolidar"
---

----------
REF -> Referência bibliográfica, deve ser colocada em ABNT, já, eu colocarei REF(nome) quando já souber, se não souber, você puxa

ORDER -> Uma instrução/seção a ser adicionada, pesquisa a ser feita

DOWNLOAD -> Busque pelo documento e salve em docs/papers, marque o ícone de check se já estiver

PDF -> gere com  /md2pdf docs/adjudicators.md
       O bloco `pdf:` do frontmatter acima controla título, autor, saída e o que remover.
       remover: andaime | andaime+notas | nada      referencias: consolidar | inline
       Todo este bloco de legenda, os sufixos DOWNLOAD ✔/✖, os colchetes de nota
       operacional e o wrapper ORDER(...) somem no PDF. O conteúdo permanece.
------------

# Adjudicadores — os votos dos ministros como decisão sobre o AF das partes

Documento companheiro de `docs/cif_lrc.md` e `docs/preferences.md`. Fixa como o modelo de
diálogos de adjudicação de Prakken (2008) se articula com a separação modular CIF/LRC e com
o modelo de perspectivas do `protocol.md`, de modo que os votos dos ministros ocupem o papel
de adjudicadores.

REF: PRAKKEN, Henry. A formal model of adjudication dialogues. Artificial Intelligence and Law, v. 16, n. 4, p. 305-328, 2008. DOWNLOAD ✔ [`bib/Prakken2008-adjudication.pdf`]

> **Nota de verificação.** O PDF em `docs/papers/` é o *manuscrito aceito* ("Artificial
> Intelligence and Law manuscript No. — will be inserted by the editor"), sem volume,
> número nem paginação finais. Os dados `v. 16, n. 4, p. 305-328` **não foram conferidos em
> fonte primária**. Conferir antes de citar. O paper declara-se extensão revista e
> simplificada de PRAKKEN (2001b).

REF: PRAKKEN, Henry; SARTOR, Giovanni. Argument-based extended logic programming with defeasible priorities. Journal of Applied Non-classical Logics, v. 7, n. 1-2, p. 25-75, 1997. DOWNLOAD ✖ [é a lógica em que as *prioridades* são elas próprias derrotáveis e argumentáveis — base técnica do §5]

REF: PRAKKEN, Henry; SARTOR, Giovanni. Formalising arguments about the burden of persuasion. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 11., 2007. Proceedings [...]. Nova York: ACM Press, 2007. p. 97-106. DOWNLOAD ✖ [**aquisição prioritária** — ver §8.4]

REF: PRAKKEN, Henry; REED, Chris; WALTON, Douglas. Dialogues about the burden of proof. In: INTERNATIONAL CONFERENCE ON ARTIFICIAL INTELLIGENCE AND LAW, 10., 2005. Proceedings [...]. Nova York: ACM Press, 2005. p. 115-124. DOWNLOAD ✖

REF: PRAKKEN, Henry; SARTOR, Giovanni. Presumptions and burdens of proof. In: JURIX 2006: THE NINETEENTH ANNUAL CONFERENCE. Legal Knowledge and Information Systems. Amsterdã: IOS Press, 2006. p. 21-30. DOWNLOAD ✖

REF: PRAKKEN, Henry; VREESWIJK, Gerard. Logics for defeasible argumentation. In: GABBAY, Dov; GÜNTHNER, Franz (Ed.). Handbook of philosophical logic. 2. ed. Dordrecht: Kluwer, 2002. v. 4, p. 219-318. DOWNLOAD ✖

[Os dados de PRAKKEN & SARTOR 1997/2006/2007, PRAKKEN, REED & WALTON 2005 e PRAKKEN & VREESWIJK 2002 foram transcritos da lista de referências do próprio Prakken (2008) e convertidos para ABNT. Não conferidos em fonte primária.]

---

## 1. O modelo de Prakken (2008) em uma página

O paper estende os modelos de diálogo de persuasão de **duas** partes com um **terceiro
jogador neutro**, para dar conta realista do papel do juiz. `Players = {π, δ, α}` — autor,
réu e adjudicador.

A crítica que motiva o paper (§1) é a de que, na literatura de AI & Law até então, o papel
do juiz ou não era modelado, ou se limitava a regular a vez de falar, ou a dizer "verdadeiro"
/ "falso" sobre as alegações. E há uma razão estrutural para o modelo de persuasão não servir:

> *"In persuasion as modelled in argumentation theory the disagreeing parties are in full
> control of the outcome: if they do not want to admit that they are wrong, they cannot be
> forced to do so. In legal procedures, by contrast, the outcome ultimately depends on the
> adjudicator's decision, so in legal procedures the disagreeing parties should not persuade
> each other but the adjudicator."*

**As duas fases.** A estrutura central do modelo:

| | **Fase de argumentação** | **Fase de decisão** |
|---|---|---|
| Quem se move | π e δ; α intervém entre turnos | **somente α** |
| Papel de α | largamente mediador | decide o conflito |
| Lances de α | `illegal`, `burden`, `terminate`, `pass` | `argue`, `terminate` |
| Objeto | construir o grafo de argumentos | avaliar o grafo construído |
| Ônus relevante | **produção** | **persuasão** |

**Ordem dos turnos.** O diálogo começa com o `claim` do autor, que assume papel de proponente.
Encerrado o turno de um adversário, a vez passa a α, que (i) decide sobre a correção
processual dos lances do turno anterior, (ii) pode alocar o ônus da produção sobre
proposições disputadas e (iii) decide se encerra a fase de argumentação. Se o diálogo
continua, a vez passa **ao perdedor corrente**. Na fase de decisão a vez é sempre de α
(regra T5).

**Uma peculiaridade técnica importante.** Prakken observa (§4.3) que a fase de decisão
*não cabe* no arcabouço geral, porque é um monólogo e porque α **pode responder aos próprios
lances** — a proibição geral de responder a si mesmo é suspensa ali. E dá a razão jurídica:

> *"This makes sense since sometimes a decision takes the form of an internal debate, such as
> 'in general, in cases like these p holds but in this case there is an exception'."*

Isso é exatamente a forma de um voto de ministro brasileiro. O voto é um monólogo
auto-dialético.

---

## 2. O erro a evitar: perspectiva não é módulo

Antes de tudo, uma decisão de arquitetura que precisa estar fixada, porque errá-la
inviabiliza o objetivo.

A tentação é tratar cada perspectiva como um módulo — `CIF_recorrente`, `CIF_recorrido`,
`LRC_relator`, e assim por diante. **Isso destrói o objeto de estudo.** Ver `cif_lrc.md`
§2.3(a):

> Nenhum argumento do CIF ataca argumento do LRC, e vice-versa. A relação de ataque não
> atravessa a fronteira. O único canal é a regra-ponte.

Essa propriedade vale para **qualquer** par de módulos na arquitetura de Prakken & Sartor
(2023): módulos não trocam ataques, trocam saídas por regras output-input. Portanto:

> **Se cada perspectiva virar um módulo, as perspectivas deixam de poder se atacar — que é
> precisamente o framework de argumentação entre perspectivas que se quer construir.**

A modelagem correta:

- **um único AF por módulo**, povoado por todas as perspectivas;
- **perspectiva = rótulo de proveniência** em cada premissa e cada regra, não compartimento;
- o conflito entre partes se resolve pelas relações de ataque normais do ASPIC+ — *rebut*,
  *undermine*, *undercut* — dentro de cada módulo;
- o conflito entre adjudicadores se resolve, ou não se resolve, no **metanível** (§5).

O schema atual já carrega o rótulo: `user_id`, `assignment_id`, `vote_or_author`,
`source_annotation_ids`.

---

## 3. Os três eixos ortogonais

O `protocol.md` colapsa em um único eixo ("perspectiva") três dimensões independentes.
Separá-las é a chave da estratégia.

```
eixo 1 — MÓDULO       que tipo de pergunta      CIF │ ponte │ LRC
eixo 2 — PERSPECTIVA  quem diz                  recorrente, recorrido, relator, min. X…
eixo 3 — PAPEL        com que autoridade diz    parte  │  adjudicador
```

Arquitetura resultante:

```
                     NÍVEL DIALÓGICO   (Prakken 2008)
   ┌───────────────────────────────┬──────────────────────────────┐
   │   fase de argumentação        │      fase de decisão         │
   │   π, δ alegam; α medeia       │      somente α se move       │
   └───────────────┬───────────────┴──────────────┬───────────────┘
                   │ produz                       │ produz
                   ▼                              ▼
        premissas e regras                undercuts, premise-attacks,
        rotuladas por perspectiva         argumentos de prioridade (≺)
                   │                              │
                   ▼                              ▼
   ┌────────────────────────────────────────────────────────────────┐
   │                        NÍVEL OBJETO                            │
   │   ┌─────────┐    ponte  oi / check    ┌─────────┐              │
   │   │   CIF   │ ───────────────────────►│   LRC   │              │
   │   └─────────┘                         └─────────┘              │
   └────────────────────────────────────────────────────────────────┘
```

**O adjudicador não é um módulo.** É um *papel* que atua no **metanível de cada módulo** e
na **ponte**. Não tem base de conhecimento própria; tem poder sobre a das partes.

---

## 4. Catálogo de atos de fala

### 4.1. Atos das partes (π, δ)

| Ato | Efeito | Campo correspondente no protocolo |
|---|---|---|
| `claim φ` | afirma φ, assume papel de proponente de φ | Posição defendida |
| `why φ` | disputa φ; exige suporte | Causas/relações contestadas |
| `concede φ` | admite φ; retira a disputa | (não previsto no formulário) |
| `retract φ` | retira alegação própria | (não previsto no formulário) |
| `argue A` | apresenta argumento, exibido como *conclusão desde premissas* | Fatos e relações causais afirmados |
| `pass` | encerra o turno; **obrigatório**, para que α reconheça o fim | — |

**Deslocamento de ônus pelas partes.** O ato `why φ` pode atacar um `why ¬φ` anterior,
exprimindo que o ônus da produção do oposto cabe ao ouvinte. Prakken atribui a ideia a
Chris Reed, via PRAKKEN, REED & WALTON (2005). Notação do complemento: `−φ`.

### 4.2. Atos do adjudicador (α) — fase de argumentação

| Ato | Efeito | Equivalente forense brasileiro |
|---|---|---|
| `illegal m` | declara o lance juridicamente inadmissível — **inclui admissibilidade de prova** | indeferimento de prova; preclusão |
| `burden(φ, p)` | aloca o **ônus da produção** de φ ao jogador `p` | distribuição do ônus da prova (CPC art. 373 e §1º) |
| `terminate` | encerra a fase de argumentação | encerramento da instrução |
| `pass` | nada a decidir | — |

`terminate` e `pass` não respondem a nenhum lance e não podem ser respondidos: seu alvo é o
valor mudo `0`.

> **Decisões procedimentais não são atacáveis pelas partes.** Prakken é explícito na conclusão:
> permitir que os adversários ataquem as decisões de α sobre legalidade de lance e ônus da
> produção descaracterizaria essas decisões como *procedimentais* — elas encerram a questão.
> E completa: isso não impede que a lei preveja recurso, **mas o procedimento recursal inicia
> um diálogo inteiramente novo, não continua o corrente**.
>
> Consequência direta para o corpus: **o julgamento do RE no STF é um diálogo de adjudicação
> novo, não a continuação do diálogo da instância de origem.** As decisões das instâncias
> anteriores entram como *material*, não como lances do mesmo jogo.

### 4.3. Atos do adjudicador — fase de decisão

Na fase de decisão α só move `argue` e `terminate`. As decisões que ele exprime são quatro
(§4.3 do paper):

| # | Decisão | Como se exprime | Se decidir "sim" |
|---|---|---|---|
| 1 | uma premissa não disputada e não atacada se sustenta? | se **não**: *premise-attack* | silêncio |
| 2 | o argumento é **internamente válido** (aceitável se não atacado)? | se **não**: **undercut** | silêncio, e passa-se a 3 |
| 3 | há razão para acrescentar contra-argumentos? | novo argumento | silêncio |
| 4 | o argumento é **dialeticamente válido** (sobrevive à competição)? | tipicamente: **argumento de prioridade** | silêncio |

E a frase que mais importa para a anotação:

> *"Note that all these decisions can be made by either remaining silent or moving an
> argument."*

> **O silêncio é decisão.** Um ministro que não faz undercut de um argumento **decidiu** que
> ele é internamente válido. Isso tem consequência prática pesada no protocolo: o campo
> "Questões não decididas" (§5.3 e §5.6) precisa distinguir *silêncio decisório* — que fixa
> o argumento — de *questão genuinamente não enfrentada*. São coisas diferentes e hoje o
> formulário não separa.

---

## 5. O voto como objeto formal

Aqui está a redução central da estratégia.

> **O voto de um ministro não é "mais uma perspectiva com suas premissas". Formalmente, o
> voto é um conjunto de *premise-attacks*, *undercuts* e **afirmações sobre `≺`**, aplicado
> ao AF construído pelas partes.**

Duas passagens sustentam isso. Em §3.2:

> *"adjudication will also be modelled as constructing arguments, typically as constructing
> **priority arguments**, which are arguments that break ties between conflicting arguments."*

E em §4.3, sobre a validade dialética:

> *"This is typically decided by **priority arguments**."*

### 5.1. Validade interna × validade dialética

A avaliação que α faz de cada argumento tem duas camadas, e elas se anotam separadamente:

| | **Validade interna** | **Validade dialética** |
|---|---|---|
| Pergunta | o argumento sustenta a conclusão *na ausência* de contra-argumentos? | ele sobrevive à competição com os contra-argumentos internamente válidos? |
| Instrumento de α | **undercut** | **argumento de prioridade** |
| No voto, soa como | "esse fundamento não se sustenta", "a premissa não autoriza a conclusão" | "ainda que assim fosse, prevalece o argumento de X" |
| Camada | qualidade do argumento isolado | ordenação entre argumentos |

Confundir as duas é o erro de anotação mais provável neste nível. "Não acolho o argumento
porque ele é inconsistente" é **undercut**; "não acolho porque o argumento contrário pesa
mais" é **prioridade**. O segundo é o que interessa ao artigo.

### 5.2. Convergência com `docs/preferences.md`

Se o voto é, em boa parte, afirmação sobre `≺`, então **`docs/preferences.md` não é um anexo
sobre desempate: é a especificação do conteúdo dos argumentos de prioridade do adjudicador.**
A tripla lexicográfica ⟨h(r), v(r), a(r)⟩ definida lá (§4 daquele documento) é precisamente o
que um ministro afirma quando decide validade dialética.

Isso reorganiza os três documentos:

| Documento | Nível |
|---|---|
| `cif_lrc.md` | **nível objeto** — sobre o que se argumenta |
| `adjudicators.md` (este) | **nível dialógico** — quem pode fazer o quê |
| `preferences.md` | **conteúdo do metanível** — com que critério α decide `≺` |

E o maquinário para tornar as próprias prioridades argumentáveis já está em `docs/papers/`:
MODGIL & PRAKKEN (2011, 2013), citados em `preferences.md` §4. A EAF de MODGIL (2009),
mencionada lá como saída para o "limite conhecido" da ordem lexicográfica, é exatamente a
estrutura em que argumentos atacam *ataques* — ou seja, em que o desacordo entre ministros
sobre `≺` é ele próprio representável.

ORDER(fechar a integração formal: mostrar que a tripla ⟨h,v,a⟩ de preferences.md instancia o `≺` que o adjudicador afirma na fase de decisão de Prakken 2008, e verificar se a ordem lexicográfica sobrevive quando dois adjudicadores discordam — provavelmente exige EAF, não ASPIC+ com ordem fixa)

---

## 6. Adjudicar no CIF ≠ adjudicar no LRC

O adjudicador atua nos dois módulos, mas **o que ele adjudica muda**, e essa assimetria é o
encaixe entre os dois papers.

| | **Adjudicação no CIF** | **Adjudicação no LRC** |
|---|---|---|
| Objeto | fato e generalização causal | qualificação jurídica |
| Instrumento dominante | **ônus da prova + admissibilidade** | **argumentos de prioridade + escolha de doutrina** |
| Atos típicos | `burden(φ,p)`, `illegal m`, *premise-attack* | prioridade entre defesas; undercut de regra doutrinária |
| Exemplo | qual laudo prevalece; se `deFi` está provado | se `unexpected(Ma)`; se `RPL` derrota `NoFor` |
| O que a divergência revela | desacordo **probatório** | desacordo **valorativo** |
| Fonte no corpus | relatório, prova, perícia | fundamentação do voto |

O exemplo motivador inteiro de Prakken (2008) §2.2 é **probatório** — autenticidade de
assinatura, documento judicial, laudo inadmissível por intempestividade. Tudo isso é CIF.
Já a decisão final do juiz naquele mesmo exemplo — *"o fato de o réu parecer normal durante
as negociações é insuficiente para concluir que sua insanidade não podia ser conhecida do
autor: ele poderia ter consultado o registro do tribunal"* — é ataque a uma inferência de
qualificação, e portanto **LRC**.

> **Regra prática.** Se o desacordo entre votos se resolveria com mais prova, é CIF. Se
> nenhuma prova adicional o resolveria, é LRC — ou é `≺`.

---

## 7. A ponte como ato de escopo

Releia `cif_lrc.md` §3: a ponte só dispara para os pares declarados em `check(Y,Z)`, que são
"fatos fornecidos pelo usuário que declaram quais pares causa-efeito devem ser verificados".

Quem fornece `check`? No modelo de Prakken isso corresponde a um poder expressamente
adjudicatório (§2.1):

> *"defining the scope of the dispute by deciding what may and may not be taken into account"*

Logo:

> **`check(φ,ψ)` é ato processual do adjudicador, não premissa fática. Um ministro que nunca
> submete uma causa candidata ao teste NESS já a decidiu, silenciosamente.**

Isso torna anotável um fenômeno comum no STF e raramente formalizado: votos que divergem
**não** na doutrina nem nos fatos, mas em *quais causas sequer entraram na pauta do
julgamento*. É a divergência D3 do §9.

---

## 8. Os três ônus

Prakken (2008) distingue três ônus, e a distinção é uma das contribuições declaradas do paper.
Ela mapeia muito bem no processo brasileiro e precisa aparecer na anotação.

### 8.1. Ônus da produção (*burden of production*)

Qual parte deve oferecer prova sobre uma questão, em cada momento do procedimento. No modelo,
torna-se relevante quando uma alegação é disputada: define se quem alegou deve sustentar com
argumento, ou se quem disputou deve argumentar por que não vale. **Alocado por α na fase de
argumentação**, pelo ato `burden(φ, p)`.

### 8.2. Ônus da persuasão (*burden of persuasion*)

Qual parte **perde** a questão se a prova estiver equilibrada. Torna-se relevante **na fase de
decisão**. α o verifica movendo argumentos, inclusive de prioridade. Nos exemplos, Prakken
assume inicialmente que o autor tem o ônus da persuasão para todas as alegações de qualquer
jogador.

### 8.3. Ônus tático (*tactical burden*)

Não é imposto por lei nem por α: é **induzido automaticamente** pela natureza derrotável da
lógica e pelo caráter dialético do jogo, via o *status dialógico* dos lances. Se uma parte
consegue virar o status da alegação principal a seu favor, transfere à outra o ônus tático de
revertê-lo.

> **É a conciliação que o paper anuncia no resumo:** o aspecto *lógico* do ônus da prova
> (induzido pela derrotabilidade) e o aspecto *dialógico* (alocado por decisão do juiz sobre
> fundamentos jurídicos) coexistem sem se reduzirem um ao outro.

### 8.4. Limite do modelo, e o que falta comprar

Os ônus de persuasão são **dados como input** à fase de decisão — α não os *argumenta*.
Prakken indica como suprimir a limitação: trocar a lógica de base pela de **PRAKKEN & SARTOR
(2007)**, que já admite argumentos da forma `burden(φ, p) desde P`.

Para o corpus do STF isso não é opcional. A distribuição do ônus da prova é, ela própria,
objeto de fundamentação nos votos — e a distribuição dinâmica do CPC art. 373, §1º, é
literalmente uma decisão fundamentada sobre ônus. Sem PRAKKEN & SARTOR (2007) o modelo não
representa isso.

ORDER(adquirir PRAKKEN & SARTOR 2007, "Formalising arguments about the burden of persuasion", ICAIL 2007, p. 97-106 — é o que permite ao adjudicador argumentar sobre ônus em vez de recebê-lo dado; sem ele não se modela o art. 373, §1º, do CPC)

ORDER(conferir a redação do art. 373 e §1º do CPC em fonte primária antes de usar o mapeamento do §4.2 e deste parágrafo)

---

## 9. Mapeamento perspectiva → papel, e tipologia da divergência

### 9.1. Papel de cada perspectiva do `protocol.md`

| Perspectiva (`protocol.md` §5) | Papel | Lances legais |
|---|---|---|
| Recorrente | **parte** (π) | `claim`, `why`, `argue`, `concede`, `retract`, `pass` |
| Recorrido | **parte** (δ) | idem |
| Relator | **adjudicador** (α) | fase de argumentação + fase de decisão |
| Voto convergente com fundamento próprio | **adjudicador** | mesmo desfecho, `≺` ou undercuts distintos |
| Voto divergente | **adjudicador** | desfecho distinto |
| **STF — posição final** | **nenhum** — é *desfecho agregado* | — |

**O voto convergente com fundamento próprio ganha definição precisa neste modelo:** é o
adjudicador que chega ao mesmo desfecho por **conjunto diferente de undercuts e/ou ordenação
`≺` diferente**. Hoje o campo "Ponto de aproximação com o relator" / "Ponto de distinção"
captura isso em texto livre; com o modelo, vira estrutura.

### 9.2. Tipologia da divergência

A arquitetura entrega de graça uma classificação do dissenso — provavelmente o achado
empírico do artigo.

| | Camada | Natureza do desacordo | Resolve-se com |
|---|---|---|---|
| **D1** | CIF / premissa | os fatos | prova |
| **D2** | CIF / regra | a generalização causal | prova / perícia |
| **D3** | ponte / `check` | **quais causas sequer foram consideradas** | nada — é escopo |
| **D4** | LRC / premissa | a qualificação (`unexpected`, `foreseeable`, `obl`) | argumento jurídico |
| **D5** | LRC / doutrina | qual base de regras se aplica — família A (eq. 2) vs. B (eq. 9) | escolha doutrinária |
| **D6** | **`≺` / prioridade** | **mesmos fatos, mesmas regras, ordenação de valores distinta** | nada — é valor |
| **D7** | fora dos módulos | itens (3)(4)(5) da responsabilidade | — |

**D6 é o caso central.** É "mesmo direito, mesmos fatos, resultado oposto" — conflito
axiológico puro, exatamente o que a tripla ⟨h,v,a⟩ foi construída para medir. E conecta com
BENCH-CAPON: cada ministro é uma **audiência** com sua ordenação; uma tese aceita sob *toda*
ordenação é *objetivamente* aceitável, sob *alguma* é *subjetivamente* aceitável. Isso dá
leitura formal para unanimidade vs. maioria apertada — e as referências já estão em
`docs/papers/` (BENCH-CAPON 2002; ATKINSON & BENCH-CAPON 2021).

**D3 é o mais original.** Ninguém mede escopo de consideração causal; a ponte dá o instrumento.

ORDER(rodar a tipologia D1-D7 sobre 3-5 acórdãos já anotados do corpus e medir a distribuição; se D6 for frequente, é o resultado do artigo; se D1/D2 dominarem, o caso é probatório e o aparato causal rende menos do que se supõe)

---

## 10. O problema do colegiado

Esta é a lacuna do modelo e a oportunidade da tese.

**Prakken (2008) tem UM adjudicador.** `Players = {π, δ, α}`, com α singular. O paper não
trata de tribunal colegiado; a única menção a pluralidade de níveis é sobre **recurso**, e é
para dizer que recurso inicia diálogo novo (§4.2 deste documento). O STF tem onze ministros e
um desfecho agregado.

### 10.1. Três modelagens

**(a) N adjudicadores, N ordenações `≺ᵢ`, agregação por contagem.** Cada ministro adjudica o
*mesmo* AF construído pelas partes, sob sua própria ordenação. O desfecho do tribunal é
contagem, não síntese argumentativa. Fiel ao funcionamento real, casa direto com a leitura de
audiências de VAF, e preserva a estrutura do dissenso — que é o dado. **Recomendada.**

**(b) A maioria como adjudicador único.** Simples e implementável de imediato, mas descarta
exatamente a informação que o artigo quer expor.

**(c) Dois níveis: cada ministro adjudica; a proclamação agrega.** Mais fiel, bem mais caro,
e exige formalizar a agregação como um segundo jogo.

### 10.2. O paradoxo doutrinário fica mensurável

Consequência que, na minha leitura, é o argumento mais forte a favor da abordagem inteira:

> **A divisão CIF/LRC fornece exatamente a decomposição em questões que o paradoxo doutrinário
> exige.** Pode haver maioria para `caFa(φ,ψ)`, maioria para "nenhuma defesa se aplica", e
> ainda assim maioria para "não responde" — se as maiorias forem compostas por ministros
> diferentes. Sem decomposição em questões o paradoxo é invisível; com CIF/LRC mais as camadas
> de defesa (`cif_lrc.md` §6.3), ele se torna **verificável em acórdãos do STF**.

Ou seja: votação por questões (*issue-by-issue*) e votação por desfecho (*outcome-based*)
podem divergir, e o formalismo permite detectar quando divergem.

REF: KORNHAUSER, Lewis A.; SAGER, Lawrence G. The one and the many: adjudication in collegial courts. California Law Review, v. 81, n. 1, p. 1-59, 1993. DOWNLOAD ✖

REF: KORNHAUSER, Lewis A.; SAGER, Lawrence G. Unpacking the court. Yale Law Journal, v. 96, n. 1, p. 82-117, 1986. DOWNLOAD ✖

REF: LIST, Christian; PETTIT, Philip. Aggregating sets of judgments: an impossibility result. Economics and Philosophy, v. 18, n. 1, p. 89-110, 2002. DOWNLOAD ✖

> **Nota de verificação — importante.** As três referências acima foram redigidas **de
> memória**, não a partir de fonte consultada. Volume, número, páginas e ano precisam ser
> conferidos antes de qualquer citação. Dado o precedente registrado em `preferences.md`
> (referência inexistente que circulava como verdadeira), tratar estas três como **não
> confirmadas** até verificação.

ORDER(verificar as três referências acima em fonte primária — Kornhauser & Sager 1986 e 1993, List & Pettit 2002 — e levantar se há literatura de AI & Law que já tenha cruzado paradoxo doutrinário com argumentação formal; se não houver, isso reforça a originalidade e precisa ser dito no artigo)

ORDER(verificar se o STF vota por questões ou por desfecho nos casos do corpus, e se a distinção aparece na ata/proclamação de resultado — é o dado que decide se o paradoxo é observável na prática)

---

## 11. Consequências para o protocolo e o schema

### 11.1. Falta o eixo 3

Há três níveis de "quem" no sistema, e só dois estão representados:

| Nível | O que é | Onde está |
|---|---|---|
| **anotador** | quem reconstruiu — epistêmico, **fora** do modelo jurídico | `user_id`, `assignment_id` ✔ |
| **perspectiva** | posição no caso | `vote_or_author`, `Perspective` ✔ |
| **papel dialógico** | parte × adjudicador | **ausente** ✖ |

Sem o terceiro nível não se sabe quais lances são legais para cada perspectiva — e, pior, o
anotador registra o voto do ministro como se fosse alegação de parte, perdendo que ele é
undercut mais prioridade.

**Proposta mínima.** Acrescentar a `Perspective` um campo `papel_dialogico`, com valores em
português conforme a convenção do projeto:

```
papel_dialogico : "parte" | "adjudicador" | "desfecho"
```

- `parte` — recorrente, recorrido
- `adjudicador` — relator, votos convergentes, votos divergentes
- `desfecho` — STF posição final (não aceita premissas próprias)

E, nas perspectivas de papel `adjudicador`, tipar o registro do voto em três listas em vez de
texto livre: *premise-attacks*, *undercuts*, *prioridades*.

### 11.2. "STF — posição final" não é perspectiva

É desfecho computado a partir dos adjudicadores. Se o anotador preencher como perspectiva com
premissas próprias, perde-se a capacidade de verificar se o resultado é **acarretado** pelas
posições individuais — que é justamente o teste do §10.2. Mesmo tipo de problema já apontado
em `cif_lrc.md` §8.1 para "causas candidatas rejeitadas".

### 11.3. "Questões não decididas" precisa separar silêncio de omissão

Ver §4.3: silêncio de α **é decisão** (fixa a validade interna do argumento). Questão não
enfrentada é outra coisa. O campo atual funde as duas.

### 11.4. Faltam `concede` e `retract`

O formulário não tem onde registrar concessão nem retratação, e ambos alteram o grafo:
concessão remove a disputa, retratação remove a alegação. Em acórdãos aparecem como
"incontroverso nos autos", "a parte não impugna", "matéria não devolvida".

ORDER(avaliar as quatro mudanças de §11 no protocol.md e em backend/models.py; lembrar que qualquer alteração de modelo exige recriar data/jurix.db, incluindo os sidecars -wal e -shm, pois não há migração)

---

## 12. Lacunas conhecidas

Duas afirmações deste documento **não** foram verificadas em fonte primária:

1. **PRAKKEN & SARTOR (2023)**, a arquitetura modular, não está em `docs/papers/` — já era a
   aquisição prioritária do `cif_lrc.md`. A tese de que a *especificação de problema de
   metanível* pode hospedar os atos adjudicatórios de escopo (`check`, §7) e de escolha de
   doutrina (D5) é **inferência** a partir do resumo dado pelo ICAIL 2026, que declara
   expressamente não recitar as definições de [26].
2. **PRAKKEN & SARTOR (2007)** é o que falta para o adjudicador argumentar sobre ônus (§8.4).

---

## 13. Resumo operacional

1. **Perspectiva é rótulo, não módulo.** Um AF por módulo, todas as perspectivas dentro.
2. **Parte alega; adjudicador decide.** São conjuntos de lances disjuntos.
3. **O voto é undercut + premise-attack + prioridade** sobre o AF das partes — não é um novo
   corpo de premissas.
4. **Undercut ≠ prioridade.** "Não se sustenta" é validade interna; "cede ao argumento
   contrário" é validade dialética. O segundo é o dado do artigo.
5. **Silêncio é decisão.**
6. **`check(φ,ψ)` é ato de escopo do adjudicador.**
7. **Adjudicar no CIF é sobre prova; no LRC é sobre valor.** Se mais prova resolveria, é CIF.
8. **"STF — posição final" é desfecho, não perspectiva.**
9. **Recurso é diálogo novo**, não continuação — o RE no STF não continua o jogo de origem.
10. **Prakken 2008 tem um adjudicador; o STF tem onze.** A extensão para colegiado é a
    contribuição a reivindicar.

---

## Anexo — aquisições pendentes, em ordem de prioridade

```
PRAKKEN & SARTOR 2023  - A formal framework for combining legal reasoning methods (ICAIL, p. 227-236)
                         arquitetura modular; sustenta cif_lrc.md §1 e este §7
PRAKKEN & SARTOR 2007  - Formalising arguments about the burden of persuasion (ICAIL, p. 97-106)
                         sem ele o adjudicador não argumenta sobre ônus — §8.4
PRAKKEN & SARTOR 1997  - Argument-based extended logic programming with defeasible priorities
                         (J. Applied Non-classical Logics 7, 25-75) — prioridades derrotáveis, §5
PRAKKEN, REED & WALTON 2005 - Dialogues about the burden of proof (ICAIL, p. 115-124)
KORNHAUSER & SAGER 1993 - The one and the many (Cal. L. Rev. 81, 1-59)   [dados a conferir]
LIST & PETTIT 2002      - Aggregating sets of judgments (Econ. & Phil. 18, 89-110)  [dados a conferir]
PRAKKEN & SARTOR 2006   - Presumptions and burdens of proof (JURIX, p. 21-30)
```

Já em `docs/papers/` e diretamente relevantes a este documento:

```
2008_Prakken_FormalModel_AILaw.pdf            fonte deste documento
PRAKKEN_SARTOR_1996_dialectical_model_AILaw.pdf   modelo dialético; antecedente de 2008
MODGIL_PRAKKEN_2011_Revisiting_Preferences_and_Argumentation_IJCAI.pdf   argumentar sobre ≺
MODGIL_PRAKKEN_2013_General_account_argumentation_with_preferences_AIJ.pdf
BENCH-CAPON_2002_Value_Based_Argumentation_Frameworks_NMR.pdf   audiências → §9.2 D6
ATKINSON_BENCH-CAPON_2021_Value-based_argumentation_survey_JAL.pdf
```
