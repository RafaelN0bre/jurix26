# Diagramas

## 0. Destino no artigo

Os dois diagramas deste arquivo são documentação de trabalho: registram o
conteúdo completo e não cabem, como estão, em figura de artigo. O mapa proposto
(numeração de tabelas e figuras conforme `plano-secao-4.md`, §II.T):

| Fonte aqui | No artigo | Forma recomendada |
|---|---|---|
| §1, etapas 1–3 | figura da 4.1 — pipeline compacto: três dossiês → grade de comparação → exercício manual conjunto → registro executável, com a distinção visual derivação (seta cheia) × consulta (seta tracejada) e o vínculo único de evidência | TikZ, meia coluna |
| §1, campos do formulário | não vira figura — a prosa de II.4.1 já os descreve | — |
| §2, ordem de execução (3 fases) | figura F3 da 4.4 — as duas ordens lado a lado (CIF→LRC × LRC→CIF→LRC), só blocos e pontes, sem conteúdo de regra | TikZ, meia coluna |
| §2, tabelas premissa/regra × perspectiva | tabela T4 da 4.3 | tabela LaTeX (booktabs), não figura |
| §2, grafo de ataques | figura F1 da 4.3 | Graphviz já gerado (`figures/case-003-final-lrc.*`), polir rótulos |
| §2, extensão fundada em 7 passos | prosa de II.4.3 (parágrafo da extensão fundamentada) | — |

Os blocos Mermaid abaixo são espelhos degradados dos ASCII — perdem o
alinhamento tabular e a distinção tipográfica entre suporte, ataque e consulta —
e não devem ser fonte de nenhuma figura. Para as figuras finais, gerar TikZ a
partir dos ASCII; para leitura rápida em docs, o ASCII é a forma canônica.

## 1. Anotação, consolidação e formalização

### ASCII

```text
  ╔════════════════════════════════════════════════════════════════════════╗
  ║ ETAPA 1 — ANOTAÇÃO AD HOC                 três juristas, em isolamento ║
  ╚════════════════════════════════════════════════════════════════════════╝

  1.1  RECONSTRUÇÃO POR PERSPECTIVAS

  ┌────────────────────────────────────────────────────────────────────────┐
  │ papel         perspectiva                                              │
  ├────────────────────────────────────────────────────────────────────────┤
  │ parte         Recorrente                                               │
  │ parte         Recorrido                                                │
  │ adjudicador   Relator                                                  │
  │ adjudicador   Voto convergente                                         │
  │ adjudicador   Voto divergente                                          │
  │ desfecho      STF — posição final                                      │
  └────────────────────────────────────────────────────────────────────────┘
                                      │
                      os mesmos campos, em cada perspectiva
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ Posição defendida    ·   Fundamento próprio    ·   Conclusão           │
  │ Fatos relevantes invocados                                             │
  │                                                                        │
  │ Causas candidatas                  ┐                                   │
  │ Causas juridicamente relevantes    ├──  afirmadas · contestadas ·      │
  │ Relações causais                   ┘    consideradas · rejeitadas      │
  │                                                                        │
  │ Razões da rejeição                                                     │
  │ Ponto de aproximação   ·   Ponto de divergência e sua razão            │
  │ Questões não decididas                                                 │
  │                                                                        │
  │ Passagens principais  ──────►  trecho do inteiro teor, com             │
  │                                documento, página, folha e voto         │
  └────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌─────────────────────────────────┐    ┌─────────────────────────────────┐
  │ 1.2  UNIDADES CAUSAIS           │    │ 1.3  DIVERGÊNCIAS               │
  ├─────────────────────────────────┤    ├─────────────────────────────────┤
  │ Causa candidata                 │    │ Ponto de divergência            │
  │ Resultado                       │    │ Perspectiva 1  ×  Perspectiva 2 │
  │ Relação causal                  │    │ O que sustenta cada uma         │
  │ Conclusão sustentada            │    │ Razão da divergência            │
  │ Perspectiva / origem            │    │ Efeito sobre a conclusão        │
  │ Status no julgamento            │    │ Passagens principais            │
  │ Tratamento pelo Tribunal        │    │                                 │
  │ Passagens principais            │    │                                 │
  └────────────────┬────────────────┘    └────────────────┬────────────────┘
                   └──────────────────┬───────────────────┘
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ 1.4  SÍNTESE                                                           │
  ├────────────────────────────────────────────────────────────────────────┤
  │ Questão central                                                        │
  │ Unidades causais                                                       │
  │ Premissas comuns         ·   Premissas controvertidas                  │
  │ Conclusão vencedora      ·   Conclusões vencidas                       │
  │ Ambiguidades             ·   Questões não decididas                    │
  └────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ DOSSIÊS CONGELADOS      dossiê A  ·  dossiê B  ·  dossiê C             │
  └────────────────────────────────────────────────────────────────────────┘


  ╔════════════════════════════════════════════════════════════════════════╗
  ║ ETAPA 2 — COMPARAÇÃO                as três reconstruções, lado a lado ║
  ╚════════════════════════════════════════════════════════════════════════╝

           dossiê A               dossiê B               dossiê C
               │                      │                      │
               └──────────────────────┬──────────────────────┘
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ GRADE COMUM                                          32 células        │
  ├────────────────────────────────────────────────────────────────────────┤
  │ 1  Fatos relevantes             5    Nexo causal                       │
  │ 2  Causas fáticas candidatas    6    Cenários causais                  │
  │ 3  Causas jurid. relevantes     7.1  Pontos de divergência             │
  │ 4  Teoria jurídica              7.2  Posturas                          │
  │                                                                        │
  │ seis seções por perspectiva, 5 células cada       =  30                │
  │ duas seções de campo livre, 1 célula cada         =   2                │
  │                                                                        │
  │ Recorrente · Recorrido · Marco Aurélio · Edson Fachin ·                │
  │ Alexandre de Moraes                                                    │
  │                                                                        │
  │ divergem em 23 das 32 células                                          │
  └────────────────────────────────────────────────────────────────────────┘


  ╔════════════════════════════════════════════════════════════════════════╗
  ║ ETAPA 3 — FORMALIZAÇÃO                   exercício manual, em conjunto ║
  ╚════════════════════════════════════════════════════════════════════════╝

  ┌────────────────────────────────────────────────────────────────────────┐
  │ BASE DE PESQUISA E CONSULTA                                            │
  ├────────────────────────────────────────────────────────────────────────┤
  │ dossiê A  ·  dossiê B  ·  dossiê C                                     │
  │ grade comparativa das três reconstruções                               │
  │ inteiro teor do acórdão                                                │
  └────────────────────────────────────────────────────────────────────────┘
                                      ╎
                                        consulta, sem derivação
                                      ╎
                                      ▽
  ┌────────────────────────────────────────────────────────────────────────┐
  │ EXERCÍCIO MANUAL, EM CONJUNTO                                          │
  ├────────────────────────────────────────────────────────────────────────┤
  │ leitura das anotações e do acórdão                                     │
  │ escolha de átomos, regras, perspectivas e ataques                      │
  │ discussão e ajuste ad hoc                                              │
  └────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ FORMALIZAÇÃO OFICIAL                                                   │
  ├────────────────────────────────────────────────────────────────────────┤
  │ átomos das duas camadas                                                │
  │ regras, por camada e por perspectiva                                   │
  │ grafo de ataques, por fase do diálogo                                  │
  └────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ REGISTRO EXECUTÁVEL                                                    │
  └────────────────────────────────────────────────────────────────────────┘

  ║  único vínculo literal entre a etapa 1 e a etapa 3: os identificadores
  ║  de trecho de um dos dossiês entram como evidência dos átomos, e cada
  ║  átomo segue rastreável até a página do acórdão


  ┌────────────────────────────────────────────────────────────────────────┐
  │ ▼   derivação        ▽   consulta, sem derivação        ║   evidência  │
  └────────────────────────────────────────────────────────────────────────┘
```
### Mermaid

```mermaid
graph TB

  subgraph E1["ETAPA 1 - ANOTACAO AD HOC - tres juristas, em isolamento"]
    A1["1.1 RECONSTRUCAO POR PERSPECTIVAS<br/><br/>parte - Recorrente<br/>parte - Recorrido<br/>adjudicador - Relator<br/>adjudicador - Voto convergente<br/>adjudicador - Voto divergente<br/>desfecho - STF, posicao final"]
    A2["OS MESMOS CAMPOS, EM CADA PERSPECTIVA<br/><br/>Posicao defendida - Fundamento proprio - Conclusao<br/>Fatos relevantes invocados<br/>Causas candidatas<br/>Causas juridicamente relevantes<br/>Relacoes causais<br/>afirmadas - contestadas - consideradas - rejeitadas<br/>Razoes da rejeicao<br/>Ponto de aproximacao - Ponto de divergencia<br/>Questoes nao decididas<br/>Passagens principais"]
    A3["1.2 UNIDADES CAUSAIS<br/><br/>Causa candidata - Resultado<br/>Relacao causal<br/>Conclusao sustentada<br/>Perspectiva de origem<br/>Status no julgamento<br/>Tratamento pelo Tribunal<br/>Passagens principais"]
    A4["1.3 DIVERGENCIAS<br/><br/>Ponto de divergencia<br/>Perspectiva 1 x Perspectiva 2<br/>O que sustenta cada uma<br/>Razao da divergencia<br/>Efeito sobre a conclusao<br/>Passagens principais"]
    A5["1.4 SINTESE<br/><br/>Questao central - Unidades causais<br/>Premissas comuns x controvertidas<br/>Conclusao vencedora x vencidas<br/>Ambiguidades - Questoes nao decididas"]
    DOS["DOSSIES CONGELADOS<br/>dossie A - dossie B - dossie C"]
  end

  subgraph E2["ETAPA 2 - COMPARACAO - as tres reconstrucoes, lado a lado"]
    B1["GRADE COMUM - 32 celulas<br/><br/>seis secoes por perspectiva, 5 celulas cada = 30<br/>duas secoes de campo livre, 1 celula cada = 2<br/><br/>1 Fatos relevantes - 2 Causas faticas candidatas<br/>3 Causas juridicamente relevantes - 4 Teoria juridica<br/>5 Nexo causal - 6 Cenarios causais<br/>7.1 Pontos de divergencia - 7.2 Posturas<br/><br/>Recorrente - Recorrido - Marco Aurelio<br/>Edson Fachin - Alexandre de Moraes<br/><br/>divergem em 23 das 32 celulas"]
  end

  subgraph E3["ETAPA 3 - FORMALIZACAO - exercicio manual, em conjunto"]
    C1["EXERCICIO MANUAL, EM CONJUNTO<br/><br/>leitura das anotacoes e do acordao<br/>escolha de atomos, regras, perspectivas e ataques<br/>discussao e ajuste ad hoc"]
    C2["FORMALIZACAO OFICIAL<br/><br/>atomos das duas camadas<br/>regras, por camada e por perspectiva<br/>grafo de ataques, por fase do dialogo"]
    C3["REGISTRO EXECUTAVEL"]
  end

  PDF["INTEIRO TEOR DO ACORDAO<br/>RE 608.880/MT - Tema 362"]

  A1 --> A2
  A2 --> A3
  A2 --> A4
  A3 --> A5
  A4 --> A5
  A5 --> DOS
  DOS --> B1
  C1 --> C2
  C2 --> C3

  PDF -.->|"cada campo vinculado a um trecho:<br/>documento, pagina, folha, voto"| A2

  DOS -.->|consulta| C1
  B1  -.->|consulta| C1
  PDF -.->|consulta| C1

  DOS ==>|"unico vinculo literal:<br/>identificadores de trecho<br/>como evidencia dos atomos"| C3
```

### SVG

<img src="figures/anotacao-etapas.svg" alt="As tres etapas: anotacao ad hoc, comparacao e formalizacao" width="100%">

## 2. Formalização — átomos, premissas e regras, por perspectiva

### ASCII

```text
  ╔══════════════════════════════════════════════════════════════════════╗
  ║ PERSPECTIVAS                                                         ║
  ╚══════════════════════════════════════════════════════════════════════╝

  RTE   Recorrente — Estado do Mato Grosso           parte
  RDO   Recorrido — família da vítima                parte
  MA    Marco Aurélio, relator                       adjudicador
  EF    Edson Fachin, voto convergente               adjudicador
  AM    Alexandre de Moraes, voto divergente         adjudicador

  ●  sustenta     ·  não sustenta     comum  nenhuma perspectiva disputa


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ ORDEM DE EXECUÇÃO —  LRC → CIF → LRC                                 ║
  ╚══════════════════════════════════════════════════════════════════════╝

  A camada de relevância roda duas vezes. Das onze regras dela, dez não
  leem literal de ponte e podem ser avaliadas antes dos fatos; só cf2lrc_q5,
  que lê CaFa, espera o resultado causal.

     fase 1   LRC, qualificação      10 regras, sem cf2lrc_q5
                   │
                   │  ponte A:  as qualificações derivadas entram
                   │            em K_n do CIF   —  acréscimo nosso
                   ▼
     fase 2   CIF, causa de fato     r0–r4
                   │
                   │  ponte B:  CaFa e ButFor justificados entram
                   │            em K_n da LRC   —  equação (1) do artigo
                   ▼
     fase 3   LRC, ponte e imputação   cf2lrc_q5 e o grafo completo

  A ordem do artigo é só CIF → LRC, com a ponte B. A ponte A é o que este
  trabalho acrescenta, e a Seção 4.4 mede o seu efeito.


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ FASE 1 — LRC, qualificação                                           ║
  ╚══════════════════════════════════════════════════════════════════════╝

  entra    K_p da LRC:  OmiEstatal, RegFechado, LapsoTemp, FormacaoQuad,
                        Latrocinio, ¬ProvCabiveis
  roda     as dez regras que não leem literal de ponte

  deriva   DeverEspec       dever específico de custódia
           AtoTerceiro      causa superveniente independente
           OmissaoGen       omissão qualificada como genérica

  também conclui ¬suca_q3, ¬sc_q6 e ¬cf2lrc_q5 — nomes de regra, não
  fatos do mundo. Não atravessam a ponte A: o CIF não tem regra com esses
  nomes para sofrer undercut, e a fase 3 os rededuz por conta própria

  sai pela ponte A   DeverEspec · AtoTerceiro · OmissaoGen   →  K_n do CIF


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ FASE 2 — CIF, causa de fato                                          ║
  ╚══════════════════════════════════════════════════════════════════════╝

  átomos
  ──────────────────────────────────────────────────────────────────────
  OmiEstatal     omissão estatal na custódia do preso     fato       K_p
  RegFechado     preso em regime prisional fechado        fato       K_p
  FugaPreso      fuga do detento                          intermed.
  Latrocinio     roubo seguido de morte pelo foragido     intermed.
  MorteVitima    morte da vítima                          intermed.
  Danos          danos materiais e morais à família       resultado

  K_n   AtoTerceiro, DeverEspec, OmissaoGen        vindos da fase 1
  K_p   OmiEstatal, RegFechado

  regras                                         RTE RDO  MA  EF  AM
  ──────────────────────────────────────────────────────────────────────────
  r0    OmiEstatal ⇒ FugaPreso                     ·   ●   ·   ·   ·
  r1    OmiEstatal ∧ RegFechado ⇒ FugaPreso        ·   ·   ●   ●   ●
  r2    FugaPreso ⇒ Latrocinio                     ●   ●   ●   ●   ●   comum
  r3    Latrocinio ⇒ MorteVitima                   ●   ●   ●   ●   ●   comum
  r4    MorteVitima ⇒ Danos                        ●   ●   ●   ●   ●   comum

  ataques nesta camada:  nenhum

  nenhuma das cinco regras lê AtoTerceiro, DeverEspec ou OmissaoGen — o
  quadro jurídico chega e não é consumido. É esse o achado da Seção 4.4

  sai pela ponte B   CaFa e ButFor de OmiEstatal, FugaPreso, Latrocinio
                     e RegFechado sobre Danos  —  sete literais


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ FASE 3 — LRC, ponte e imputação                                      ║
  ╚══════════════════════════════════════════════════════════════════════╝

  átomos
  ──────────────────────────────────────────────────────────────────────
  LapsoTemp      crime três meses após a fuga             fato       K_p
  FormacaoQuad   crime em concurso de agentes             fato       K_p
  Latrocinio     roubo seguido de morte                   fato       K_p
  ¬ProvCabiveis  Estado não adotou as cautelas devidas    prova      K_p
  DeverEspec     dever específico de custódia             dever      fase 1
  OmissaoGen     omissão qualificada como genérica        dever      fase 1
  AtoTerceiro    causa superveniente independente         intermed.  fase 1
  PremedAlvo     crime premeditado contra alvo certo      fato       ✗
  SeqImediata    sequência imediata entre fuga e crime    fato       ✗
  MeiosDisp      Estado tinha meios materiais             prova      ✗

  ✗   em L e fora de K. PremedAlvo e SeqImediata são o distinguishing do
      RE 136.247, que a teoria do acórdão enuncia e estes autos não
      realizam; MeiosDisp é o requisito de meios do teste do dever, que
      voto nenhum chega a afirmar

  K_n   os sete literais de ponte vindos da fase 2; só
        CaFa(OmiEstatal, Danos) é lido por regra

  premissas de K_p                               RTE RDO  MA  EF  AM
  ──────────────────────────────────────────────────────────────────────────
  OmiEstatal                                       ·   ●   ●   ●   ●
  RegFechado                                       ·   ●   ●   ●   ·
  LapsoTemp                                        ●   ·   ·   ·   ●
  FormacaoQuad                                     ·   ·   ·   ·   ●
  Latrocinio                                       ●   ●   ●   ●   ●   comum
  ¬ProvCabiveis                                    ·   ·   ·   ●   ·

  regras                                         RTE RDO  MA  EF  AM
  ──────────────────────────────────────────────────────────────────────────
  dvesp_q0   RegFechado ⇒ DeverEspec               ·   ●   ●   ●   ·   ext.
  suca_q3    LapsoTemp ⇒ AtoTerceiro               ●   ·   ·   ·   ·   eq.5
  u_corte    LapsoTemp ⇒ ¬suca_q3                  ·   ·   ·   ·   ●   ext.
  suca_q4                                          ·   ·   ·   ·   ●   eq.5
             Latrocinio ∧ LapsoTemp ∧ FormacaoQuad ⇒ AtoTerceiro
  q_reab     PremedAlvo ∧ SeqImediata ⇒ ¬suca_q4   ·   ·   ·   ·   ●   ext.
  cf2lrc_q5  CaFa(OmiEstatal,Danos) ⇒ LeReCa(…)    ·   ●   ●   ●   ·   eq.2
  sc_q6      AtoTerceiro ⇒ ¬cf2lrc_q5              ●   ·   ·   ·   ●   eq.4
  dvpre_q8   DeverEspec ⇒ ¬sc_q6                   ·   ·   ●   ●   ·   ext.
  og_q9                                            ·   ·   ·   ·   ●   ext.
             OmiEstatal ∧ LapsoTemp ∧ FormacaoQuad ⇒ OmissaoGen
  og_q10     OmissaoGen ⇒ ¬cf2lrc_q5               ·   ·   ·   ·   ●   ext.
  q11        ¬ProvCabiveis ⇒ ¬suca_q3              ·   ·   ·   ●   ·   ext.

  eq.   esquema de Pisano et al. (2026)     ext.   extensão deste trabalho
  só cf2lrc_q5 é nova nesta fase; as dez restantes já rodaram na fase 1


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ GRAFO DE ATAQUES — todos de undercutting                             ║
  ╚══════════════════════════════════════════════════════════════════════╝

  FASE DE ARGUMENTAÇÃO — partes
  ──────────────────────────────────────────────────────────────────────
  RTE    suca_q3 ⟹ AtoTerceiro ⟹ sc_q6      ⇏  cf2lrc_q5
         prevalece por default dialético: não recebeu réplica

  FASE DE DECISÃO — adjudicadores
  ──────────────────────────────────────────────────────────────────────
  MA     dvpre_q8                           ⇏  sc_q6
  EF     dvpre_q8                           ⇏  sc_q6
         q11                                ⇏  suca_q3
  AM     u_corte                            ⇏  suca_q3     ex officio
         suca_q4 ⟹ AtoTerceiro ⟹ sc_q6      ⇏  cf2lrc_q5   caminho 1
         og_q9 ⟹ OmissaoGen ⟹ og_q10        ⇏  cf2lrc_q5   caminho 2
         q_reab                             ⇏  suca_q4     inerte

  pontos sensíveis a preferência:  nenhum


  ╔══════════════════════════════════════════════════════════════════════╗
  ║ EXTENSÃO FUNDADA DA FASE 3                                           ║
  ╚══════════════════════════════════════════════════════════════════════╝

  1   dvesp_q0 não é atacada             DeverEspec         in
  2   dvpre_q8 dispara                   sc_q6              out    ✗ cam. 1
  3   u_corte e q11 disparam             suca_q3            out
  4   og_q9 dispara dos fatos postos     OmissaoGen         in
  5   og_q10 não sofre ataque            og_q10             in
  6   og_q10 undercuta a ponte           cf2lrc_q5          out    ✓ cam. 2
  7                          LeReCa(OmiEstatal, Danos)      out

  o Estado não responde — e a tese do dever específico, vencedora onde foi
  disputada, não decide o caso: o caminho 2 não passa por ela
```
### Mermaid

```mermaid
graph TB

  subgraph F1["FASE 1 - LRC, qualificacao - 10 regras, sem cf2lrc_q5"]
    LapsoTemp["LapsoTemp"]
    FormacaoQuad["FormacaoQuad"]
    LatrocinioL["Latrocinio"]
    nProv["nao ProvCabiveis"]
    PremedAlvo["PremedAlvo<br/>fora de K"]
    SeqImediata["SeqImediata<br/>fora de K"]
    dvesp["dvesp_q0 - RDO MA EF<br/>extensao"]
    suca3["suca_q3 - RTE<br/>eq. 5 - alegacao de parte"]
    ucorte["u_corte - AM<br/>extensao - ex officio"]
    q11["q11 - EF<br/>extensao"]
    suca4["suca_q4 - AM<br/>eq. 5"]
    qreab["q_reab - AM<br/>extensao - inerte"]
    og9["og_q9 - AM<br/>extensao"]
    og10["og_q10 - AM<br/>extensao"]
    sc6["sc_q6 - RTE AM<br/>eq. 4"]
    dvpre["dvpre_q8 - MA EF<br/>extensao"]
    DeverEspec["DeverEspec"]
    OmissaoGen["OmissaoGen"]
    AtoTerceiro["AtoTerceiro"]
  end

  PA["PONTE A<br/>as qualificacoes derivadas entram em K_n do CIF<br/>DeverEspec - AtoTerceiro - OmissaoGen<br/>acrescimo deste trabalho"]

  subgraph F2["FASE 2 - CIF, causa de fato - nenhum ataque"]
    KNCIF["K_n do CIF<br/>DeverEspec - AtoTerceiro - OmissaoGen<br/><br/>nenhuma das regras r0-r4 consome<br/>estas qualificacoes: o quadro juridico<br/>chega e nao e lido"]
    OmiEstatal["OmiEstatal"]
    RegFechado["RegFechado"]
    r0["r0 - RDO"]
    r1["r1 - MA EF AM"]
    FugaPreso["FugaPreso"]
    r2["r2 - comum"]
    Latrocinio["Latrocinio"]
    r3["r3 - comum"]
    MorteVitima["MorteVitima"]
    r4["r4 - comum"]
    Danos["Danos"]
  end

  PB["PONTE B - equacao 1 do artigo<br/>CaFa e ButFor justificados entram em K_n da LRC<br/>sete literais; so CaFa OmiEstatal Danos e lido por regra"]

  subgraph F3["FASE 3 - LRC, ponte e imputacao"]
    cf2lrc["cf2lrc_q5 - RDO MA EF<br/>eq. 2 - presuncao"]
    LeReCa["LeReCa OmiEstatal Danos<br/>AFASTADA - o Estado nao responde"]
  end

  subgraph LEG["LEGENDA"]
    L1["regra so de parte"]
    L2["regra so de adjudicador"]
    L3["de parte e adjudicador"]
    L4["incontroversa"]
    L5["seta fina: suporte"]
    L6["seta grossa: ataque por undercutting"]
  end

  RegFechado --> dvesp
  dvesp --> DeverEspec
  DeverEspec --> dvpre
  LapsoTemp --> suca3
  suca3 --> AtoTerceiro
  LapsoTemp --> ucorte
  nProv --> q11
  LatrocinioL --> suca4
  LapsoTemp --> suca4
  FormacaoQuad --> suca4
  suca4 --> AtoTerceiro
  PremedAlvo --> qreab
  SeqImediata --> qreab
  AtoTerceiro --> sc6
  OmiEstatal --> og9
  LapsoTemp --> og9
  FormacaoQuad --> og9
  og9 --> OmissaoGen
  OmissaoGen --> og10

  dvpre  ==>|afasta| sc6
  ucorte ==>|afasta| suca3
  q11    ==>|afasta| suca3
  qreab  ==>|afastaria| suca4

  DeverEspec --> PA
  AtoTerceiro --> PA
  OmissaoGen --> PA
  PA --> KNCIF

  OmiEstatal --> r0
  r0 --> FugaPreso
  OmiEstatal --> r1
  RegFechado --> r1
  r1 --> FugaPreso
  FugaPreso --> r2
  r2 --> Latrocinio
  Latrocinio --> r3
  r3 --> MorteVitima
  MorteVitima --> r4
  r4 --> Danos
  Danos --> PB
  PB --> cf2lrc
  cf2lrc --> LeReCa

  sc6  ==>|"afasta - caminho 1"| cf2lrc
  og10 ==>|"afasta - caminho 2"| cf2lrc

  L5 ==>|"seta grossa"| L6

  classDef parte stroke:#c0392b,stroke-width:2px
  classDef adjud stroke:#6c3483,stroke-width:2px
  classDef misto stroke:#1f618d,stroke-width:2px
  classDef comum stroke:#707b7c,stroke-width:1px

  class r0,suca3,L1 parte
  class r1,ucorte,suca4,qreab,dvpre,og9,og10,q11,L2 adjud
  class dvesp,cf2lrc,sc6,L3 misto
  class r2,r3,r4,L4 comum
  class KNCIF comum
```

### SVG

<img src="figures/formalizacao-fases.svg" alt="As tres fases: LRC qualificacao, CIF, LRC ponte e imputacao" width="100%">
