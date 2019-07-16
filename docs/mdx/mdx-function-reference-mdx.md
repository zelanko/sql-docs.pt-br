---
title: Referência da função MDX (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff14718e09fa3732a40ea245430f33c599325eea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003506"
---
# <a name="mdx-function-reference-mdx"></a>Referência de função MDX (MDX)


  Analysis Services fornece para o uso de funções na sintaxe de MDX (Multidimensional Expressions). As funções podem ser usadas em qualquer instrução MDX válida e são frequentemente usadas em consultas, definições de acúmulos personalizados e outros cálculos. Esta seção fornece informações sobre as funções MDX.  
  
 Você pode usar as tabelas a seguir para localizar funções pela categoria dos valores retornados ou pode selecionar uma função por nome na lista alfabética, no índice.  
  
## <a name="array-functions"></a>Funções de matriz  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Settoarray=1=«conjunto &#40;MDX&#41;](../mdx/settoarray-mdx.md)|Converte um ou mais conjuntos para uma matriz para uso em uma função definida pelo usuário.|  
  
## <a name="hierarchy-functions"></a>Funções de hierarquia  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Hierarquia &#40;MDX&#41;](../mdx/hierarchy-mdx.md)|Retorna a hierarquia que contém um membro ou nível especificado.|  
|[Dimensão &#40;MDX&#41;](../mdx/dimension-mdx.md)|Retorna a dimensão que contém um membro, um nível ou uma hierarquia especificada.|  
|[Dimensões &#40;MDX&#41;](../mdx/dimensions-mdx.md)|Retorna uma hierarquia especificada por uma expressão numérica ou de cadeia de caracteres.|  
  
## <a name="level-functions"></a>Funções de nível  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Nível de &#40;MDX&#41;](../mdx/level-mdx.md)|Retorna o nível de um membro.|  
|[Níveis de &#40;MDX&#41;](../mdx/levels-mdx.md)|Retorna o nível cuja posição em uma dimensão ou hierarquia é especificada por uma expressão numérica ou cujo nome é especificado por uma expressão de cadeia de caracteres.|  
  
## <a name="logical-functions"></a>Funções lógicas  
  
|Função|Descrição|  
|--------------|-----------------|  
|[IsAncestor &#40;MDX&#41;](../mdx/isancestor-mdx.md)|Retorna se um membro especificado é um ancestral de outro membro especificado.|  
|[IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)|Retorna se a expressão avaliada for o valor de célula vazio.|  
|[IsGeneration &#40;MDX&#41;](../mdx/isgeneration-mdx.md)|Retorna se um membro especificado estiver em uma geração especificada.|  
|[IsLeaf &#40;MDX&#41;](../mdx/isleaf-mdx.md)|Retorna se um membro especificado for um membro folha.|  
|[IsSibling &#40;MDX&#41;](../mdx/issibling-mdx.md)|Retorna se um membro especificado for um irmão de outro membro especificado.|  
  
## <a name="member-functions"></a>Funções de membro  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Ancestral &#40;MDX&#41;](../mdx/ancestor-mdx.md)|Retorna o ancestral de um membro em um nível ou uma distância especificada.|  
|[ClosingPeriod &#40;MDX&#41;](../mdx/closingperiod-mdx.md)|Retorna o último irmão entre os descendentes de um membro em um nível especificado.|  
|[Primo &#40;MDX&#41;](../mdx/cousin-mdx.md)|Retorna o membro filho com a mesma posição relativa sob um membro pai como o membro filho especificado.|  
|[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)|Retorna o membro atual junto junto de uma dimensão ou hierarquia especificada durante a iteração.|  
|[DataMember &#40;MDX&#41;](../mdx/datamember-mdx.md)|Retorna o membro de dados gerado pelo sistema associado a um membro não folha de uma dimensão.|  
|[DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)|Retorna o membro padrão de uma dimensão ou hierarquia.|  
|[FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)|Retorna o primeiro filho de um membro.|  
|[FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)|Retorna o primeiro filho do pai de um membro.|  
|[Item &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)|Retorna um membro de uma tupla especificada.|  
|[Latência &#40;MDX&#41;](../mdx/lag-mdx.md)|Retorna o membro que é um número especificado de posições antes de um membro especificado junto à dimensão do membro.|  
|[LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)|Retorna o último filho de um membro especificado.|  
|[Lastsibling=2==retorna &#40;MDX&#41;](../mdx/lastsibling-mdx.md)|Retorna o último filho do pai de um membro especificado.|  
|[Levar &#40;MDX&#41;](../mdx/lead-mdx.md)|Retorna o membro que é um número especificado de posições que seguem um membro especificado junto à dimensão do membro.|  
|[LinkMember &#40;MDX&#41;](../mdx/linkmember-mdx.md)|Retorna o membro equivalente a um membro especificado em uma hierarquia especificada.|  
|[Membros &#40;cadeia de caracteres&#41; &#40;MDX&#41;](../mdx/members-string-mdx.md)|Retorna um membro especificado por uma expressão de cadeia de caracteres.|  
|[NextMember &#40;MDX&#41;](../mdx/nextmember-mdx.md)|Retorna o próximo membro no nível que contém um membro especificado.|  
|[OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)|Retorna o primeiro irmão entre os descendentes de um nível especificado, opcionalmente em um membro especificado.|  
|[ParallelPeriod &#40;MDX&#41;](../mdx/parallelperiod-mdx.md)|Retorna um membro de um período anterior na mesma posição relativa como um membro especificado.|  
|[Parent &#40;MDX&#41;](../mdx/parent-mdx.md)|Retorna o pai de um membro.|  
|[PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)|Retorna o membro anterior no nível que contém um membro especificado.|  
|[StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)|Retorna o membro especificado por uma cadeia de caracteres formatada para MDX.|  
|[UnknownMember &#40;MDX&#41;](../mdx/unknownmember-mdx.md)|Retorna o membro desconhecido associado a um nível ou membro.|  
|[ValidMeasure &#40;MDX&#41;](../mdx/validmeasure-mdx.md)|Retorna uma medida válida em um cubo virtual forçando dimensões inaplicáveis ao nível superior.|  
  
## <a name="numeric-functions"></a>Funções numéricas  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Agregação &#40;MDX&#41;](../mdx/aggregate-mdx.md)|Retorna um valor escalar calculado agregando-se medidas ou uma expressão numérica opcionalmente especificada sobre as tuplas de um conjunto especificado.|  
|[Avg &#40;MDX&#41;](../mdx/avg-mdx.md)|Retorna o valor médio de medidas ou o valor médio de uma expressão numérica opcional, avaliado sobre um conjunto especificado.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Retorna a análise de cálculo atual de um cubo para o contexto de consulta especificado.|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Retorna o valor de uma expressão MDX avaliada na fase de cálculo especificada de um cubo.|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|Transforma um valor de célula vazio em um número ou uma cadeia de caracteres e retorna o valor transformado.|  
|[Correlação &#40;MDX&#41;](../mdx/correlation-mdx.md)|Retorna o coeficiente de correlação de duas séries avaliadas sobre um conjunto.|  
|[Contagem de &#40;dimensão&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)|Retorna o número de dimensões em um cubo.|  
|[Contagem de &#40;níveis de hierarquia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)|Retorna o número de níveis em uma dimensão ou hierarquia.|  
|[Contagem de &#40;definir&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)|Retorna o número de células em um conjunto.|  
|[Contagem de &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)|Retorna o número de dimensões em uma tupla.|  
|[Covariância &#40;MDX&#41;](../mdx/covariance-mdx.md)|Retorna a covariação de população de duas séries avaliadas sobre um conjunto, usando a fórmula de população polarizada.|  
|[CovarianceN &#40;MDX&#41;](../mdx/covariancen-mdx.md)|Retorna a covariação de exemplo de duas séries avaliadas sobre um conjunto, usando a fórmula de população não polarizada.|  
|[DistinctCount &#40;MDX&#41;](../mdx/distinctcount-mdx.md)|Retorna o número de tuplas distintas, não vazias em um conjunto.|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|Retorna um de dois valores determinados por um teste lógico.|  
|[LinRegIntercept &#40;MDX&#41;](../mdx/linregintercept-mdx.md)|Calcula a regressão linear de um conjunto e retorna o valor da interceptação na linha de regressão, y = ax + b.|  
|[LinRegPoint &#40;MDX&#41;](../mdx/linregpoint-mdx.md)|Calcula a regressão linear de um conjunto e retorna o valor de *y* na linha de regressão, y = ax + b.|  
|[LinRegR2 &#40;MDX&#41;](../mdx/linregr2-mdx.md)|Calcula a regressão linear de um conjunto e retorna o coeficiente de determinação, R2.|  
|[LinRegSlope &#40;MDX&#41;](../mdx/linregslope-mdx.md)|Calcula a regressão linear de um conjunto e retorna o valor do declive na linha de regressão, y = ax + b.|  
|[LinRegVariance &#40;MDX&#41;](../mdx/linregvariance-mdx.md)|Calcula a regressão linear de um conjunto e retorna a variância associada à linha de regressão, y = ax + b.|  
|[LookupCube &#40;MDX&#41;](../mdx/lookupcube-mdx.md)|Retorna o valor de uma expressão MDX avaliada sobre outro cubo especificado no mesmo banco de dados.|  
|[Max &#40;MDX&#41;](../mdx/max-mdx.md)|Retorna o valor máximo de uma expressão numérica que é avaliada sobre um conjunto.|  
|[Mediana &#40;MDX&#41;](../mdx/median-mdx.md)|Retorna o valor mediano de uma expressão numérica que é avaliada sobre um conjunto.|  
|[Min &#40;MDX&#41;](../mdx/min-mdx.md)|Retorna o valor mínimo de uma expressão numérica que é avaliada sobre um conjunto.|  
|[Ordinal de &#40;MDX&#41;](../mdx/ordinal-mdx.md)|Retorna o valor ordinal com base em zero associado a um nível.|  
|[Prever &#40;MDX&#41;](../mdx/predict-mdx.md)|Retorna um valor de uma expressão numérica avaliada em função sobre um modelo de mineração de dados.|  
|[Classificação &#40;MDX&#41;](../mdx/rank-mdx.md)|Retorna a classificação de base um de uma tupla especificada em um conjunto especificado.|  
|[RollupChildren &#40;MDX&#41;](../mdx/rollupchildren-mdx.md)|Retorna um valor gerado pelo acúmulo dos valores dos filhos de um membro especificado usando o operador unário especificado.|  
|[Stddev &#40;MDX&#41;](../mdx/stddev-mdx.md)|Alias da [Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md).|  
|[Função StddevP &#40;MDX&#41;](../mdx/stddevp-mdx.md)|Alias da [StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md).|  
|[Stdev &#40;MDX&#41;](../mdx/stdev-mdx.md)|Retorna o desvio padrão de exemplo de uma expressão numérica, avaliado em relação a um conjunto, usando a fórmula de população não polarizada.|  
|[StdevP &#40;MDX&#41;](../mdx/stdevp-mdx.md)|Retorna o desvio padrão de população de uma expressão numérica avaliada sobre um conjunto, usando a fórmula de população polarizada.|  
|[StrToValue &#40;MDX&#41;](../mdx/strtovalue-mdx.md)|Retorna o valor especificado por uma cadeia de caracteres formatada para MDX.|  
|[Soma &#40;MDX&#41;](../mdx/sum-mdx.md)|Retorna a soma de uma expressão numérica avaliada em um conjunto.|  
|[Valor &#40;MDX&#41;](../mdx/value-mdx.md)|Retorna o valor de uma medida.|  
|[Var &#40;MDX&#41;](../mdx/var-mdx.md)|Retorna a variância de exemplo de uma expressão numérica, avaliado em relação a um conjunto, usando a fórmula de população não polarizada.|  
|[Variação de &#40;MDX&#41;](../mdx/variance-mdx.md)|Alias da [Var &#40;MDX&#41;](../mdx/var-mdx.md).|  
|[VarianceP &#40;MDX&#41;](../mdx/variancep-mdx.md)|Alias da [VarP &#40;MDX&#41;](../mdx/varp-mdx.md).|  
|[VarP &#40;MDX&#41;](../mdx/varp-mdx.md)|Retorna a variância de população de uma expressão numérica avaliada sobre um conjunto, usando a fórmula de população polarizada.|  
  
## <a name="set-functions"></a>Funções do conjunto  
  
|Função|Descrição|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)|Retorna um conjunto gerado, adicionando membros calculados a um conjunto especificado.|  
|[AllMembers=2==retorna &#40;MDX&#41;](../mdx/allmembers-mdx.md)|Retorna um conjunto que contém todos os membros, inclusive membros calculados, da dimensão, da hierarquia ou do nível especificado.|  
|[Ancestrais &#40;MDX&#41;](../mdx/ancestors-mdx.md)|Retorna um conjunto de todos os ancestrais de um membro a um nível especificado ou distância.|  
|[Ascendentes &#40;MDX&#41;](../mdx/ascendants-mdx.md)|Retorna o conjunto dos ascendentes de um membro especificado, inclusive o próprio membro.|  
|[Eixo de &#40;MDX&#41;](../mdx/axis-mdx.md)|Retorna um conjunto definido em um eixo.|  
|[BottomCount &#40;MDX&#41;](../mdx/bottomcount-mdx.md)|Classifica um conjunto na ordem crescente e retorna o número especificado de tuplas com os valores mais baixos.|  
|[BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)|Classifica um conjunto em ordem crescente e retorna um conjunto de tuplas com os valores mais baixos, cujo total cumulativo é igual ou menor do que um percentual especificado.|  
|[BottomSum &#40;MDX&#41;](../mdx/bottomsum-mdx.md)|Classifica um conjunto em ordem crescente e retorna um conjunto de tuplas com os valores mais baixos, cujo total é igual a ou menor que um valor especificado.|  
|[Children &#40;MDX&#41;](../mdx/children-mdx.md)|Retorna os filhos de um membro especificado.|  
|[Junção cruzada &#40;MDX&#41;](../mdx/crossjoin-mdx.md)|Retorna o produto cruzado de um ou mais conjuntos.|  
|[CurrentOrdinal &#40;MDX&#41;](../mdx/currentordinal-mdx.md)|Retorna o número de iteração atual dentro de um conjunto durante a iteração.|  
|[Descendentes &#40;MDX&#41;](../mdx/descendants-mdx.md)|Retorna o conjunto de descendentes de um membro em uma distância ou nível especificado, incluindo ou excluindo, opcionalmente, descendentes em outros níveis.|  
|[Distinct &#40;MDX&#41;](../mdx/distinct-mdx.md)|Retorna um conjunto, removendo tuplas duplicadas de um conjunto especificado.|  
|[DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)|Faz uma busca detalhada dos membros de um conjunto em um nível abaixo do nível mais baixo representado no conjunto ou para um nível abaixo de um nível opcionalmente especificado de um membro representado no conjunto.|  
|[Drilldownlevelbottom=1=«conjunto &#40;MDX&#41;](../mdx/drilldownlevelbottom-mdx.md)|Faz uma busca detalhada dos membros mais inferiores de um conjunto, em um nível especificado, para um nível abaixo.|  
|[Drilldownleveltop=1=«conjunto &#40;MDX&#41;](../mdx/drilldownleveltop-mdx.md)|Faz uma busca detalhada dos principais membros de um conjunto, em um nível especificado, para um nível abaixo.|  
|[DrilldownMember &#40;MDX&#41;](../mdx/drilldownmember-mdx.md)|Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado. Opcionalmente, a função faz uma busca em um conjunto de tuplas.|  
|[DrilldownMemberBottom &#40;MDX&#41;](../mdx/drilldownmemberbottom-mdx.md)|Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado, limitando o conjunto de resultado a um número especificado de membros. Opcionalmente, essa função também faz uma busca detalhada em um conjunto de tuplas.|  
|[DrilldownMemberTop &#40;MDX&#41;](../mdx/drilldownmembertop-mdx.md)|Faz uma busca detalhada dos membros de um determinado conjunto que estejam presentes em um segundo conjunto especificado, limitando o conjunto de resultado a um número especificado de membros. Opcionalmente, essa função faz uma busca detalhada em um conjunto de tuplas.|  
|[Drilluplevel=1=«conjunto &#40;MDX&#41;](../mdx/drilluplevel-mdx.md)|Faz drill up dos membros de um conjunto que estão abaixo de um nível especificado.|  
|[DrillupMember &#40;MDX&#41;](../mdx/drillupmember-mdx.md)|Faz drill up de membros em um conjunto detalhado presente em um segundo conjunto especificado.|  
|[Exceto &#40;MDX&#41;](../mdx/except-mdx-function.md)|Encontra a diferença entre dois conjuntos, enquanto retendo duplicatas opcionalmente.|  
|[Existe &#40;MDX&#41;](../mdx/exists-mdx.md)|Retorna o conjunto de membros de um conjunto que existem com uma ou mais tuplas de um ou mais conjuntos.|  
|[Extraia &#40;MDX&#41;](../mdx/extract-mdx.md)|Retorna um conjunto de tuplas dos elementos de dimensão extraídos.|  
|[Filtro &#40;MDX&#41;](../mdx/filter-mdx.md)|Retorna o conjunto resultante da filtragem de um conjunto especificado com base em um critério de pesquisa.|  
|[Gerar &#40;MDX&#41;](../mdx/generate-mdx.md)|Aplica um conjunto a cada membro de outro conjunto e une os conjuntos resultantes por união. Opcionalmente, essa função retorna uma cadeia de caracteres concatenada criada avaliando-se uma expressão de cadeia de caracteres sobre um conjunto.|  
|[Cabeçalho &#40;MDX&#41;](../mdx/head-mdx.md)|Retorna o primeiro número especificado de elementos em um conjunto, mantendo as duplicatas.|  
|[Hierarquize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)|Ordena os membros de um conjunto em uma hierarquia.|  
|[Se cruzam &#40;MDX&#41;](../mdx/intersect-mdx.md)|Retorna a interseção de dois conjuntos de entrada, mantendo as duplicatas.|  
|[LastPeriods &#40;MDX&#41;](../mdx/lastperiods-mdx.md)|Retorna um conjunto de membros até e inclusive um membro especificado.|  
|[Membros &#40;definir&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)|Retorna o conjunto de membros em uma dimensão, nível ou hierarquia.|  
|[Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)|Retorna um conjunto de membros irmão do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo nível Ano na dimensão Tempo.|  
|[NameToSet &#40;MDX&#41;](../mdx/nametoset-mdx.md)|Retorna um conjunto que contém o membro especificado por uma cadeia de caracteres formatada para MDX.|  
|[NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)|Retorna um conjunto cruzado de um ou mais conjuntos, com exceção de tuplas vazias e tuplas sem dados da tabela de fatos associados.|  
|[Ordem de &#40;MDX&#41;](../mdx/order-mdx.md)|Organiza membros de um conjunto especificado, preservando opcionalmente ou quebrando a hierarquia.|  
|[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)|Retorna um conjunto de membros irmão do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido por um nível especificado na dimensão Tempo.|  
|[Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)|Retorna os membros de um conjunto de irmãos do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo *trimestre* nível na dimensão de tempo.|  
|[Irmãos &#40;MDX&#41;](../mdx/siblings-mdx.md)|Retorna os irmãos de um membro especificado, inclusive o próprio membro.|  
|[StripCalculatedMembers &#40;MDX&#41;](../mdx/stripcalculatedmembers-mdx.md)|Retorna um conjunto gerado, removendo membros calculados de um conjunto especificado.|  
|[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)|Retorna o conjunto especificado por uma cadeia de caracteres formatada para MDX.|  
|[Subconjunto &#40;MDX&#41;](../mdx/subset-mdx.md)|Retorna um subconjunto de tuplas de um conjunto especificado.|  
|[Parte final &#40;MDX&#41;](../mdx/tail-mdx.md)|Retorna um subconjunto desde o final de um conjunto.|  
|[ToggleDrillState &#40;MDX&#41;](../mdx/toggledrillstate-mdx.md)|Alterna o estado de busca de membros.|  
|[TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)|Classifica um conjunto em ordem decrescente e retorna o número especificado de elementos com os valores mais altos.|  
|[TopPercent &#40;MDX&#41;](../mdx/toppercent-mdx.md)|Classifica um conjunto em ordem decrescente e retorna um conjunto de tuplas com os valores mais altos, cujo total cumulativo é igual ou menor que um percentual especificado.|  
|[TopSum &#40;MDX&#41;](../mdx/topsum-mdx.md)|Classifica um conjunto e retorna os elementos de nível mais alto cujo total cumulativo é pelo menos um valor especificado.|  
|[União &#40;MDX&#41;](../mdx/union-mdx.md)|Retorna a união de dois conjuntos, retendo duplicatas opcionalmente.|  
|[Unorder &#40;MDX&#41;](../mdx/unorder-mdx.md)|Remove qualquer classificação forçada de um conjunto especificado.|  
|[VisualTotals &#40;MDX&#41;](../mdx/visualtotals-mdx.md)|Retorna um conjunto gerado com a totalização dinâmica de membros filho em um conjunto especificado, utilizando, opcionalmente, um padrão para o nome do membro pai no conjunto de células resultante.|  
|[WTD &#40;MDX&#41;](../mdx/wtd-mdx.md)|Retorna um conjunto de membros irmãos do mesmo nível como um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo nível Semana na dimensão Tempo.|  
|[Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)|Retorna os membros de um conjunto de irmãos do mesmo nível de um determinado membro, começando com o primeiro irmão e terminando com um determinado membro, restringido pelo *ano* nível na dimensão de tempo.|  
  
## <a name="string-functions"></a>Funções de cadeia de caracteres  
  
|Função|Descrição|  
|--------------|-----------------|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Retorna o valor de uma expressão MDX avaliado sobre a passagem de cálculo especificada de um cubo.|  
|[CoalesceEmpty &#40;MDX&#41;](../mdx/coalesceempty-mdx.md)|Transforma um valor de célula vazio em um número ou uma cadeia de caracteres e retorna o valor transformado.|  
|[Gerar &#40;MDX&#41;](../mdx/generate-mdx.md)|Aplica um conjunto a cada membro de outro conjunto e une os conjuntos resultantes por união. Opcionalmente, essa função retorna uma cadeia de caracteres concatenada criada avaliando-se uma expressão de cadeia de caracteres sobre um conjunto.|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|Retorna um de dois valores determinados por um teste lógico.|  
|[LookupCube &#40;MDX&#41;](../mdx/lookupcube-mdx.md)|Retorna o valor de uma expressão MDX avaliada sobre outro cubo especificado no mesmo banco de dados.|  
|[MemberToStr=1=«membro»=retorna &#40;MDX&#41;](../mdx/membertostr-mdx.md)|Retorna uma cadeia de caracteres formatada para MDX que corresponde a um membro especificado.|  
|[Nome &#40;MDX&#41;](../mdx/name-mdx.md)|Retorna o nome de uma dimensão, hierarquia, nível ou membro.|  
|[Properties &#40;MDX&#41;](../mdx/properties-mdx.md)|Retorna uma cadeia de caracteres ou um valor com rigidez de tipos que contém um valor de propriedade do membro.|  
|[SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md)|Retorna uma cadeia de caracteres formatada para MDX que corresponde a um conjunto especificado.|  
|[Tupletostr=1=«tupla»=retorna &#40;MDX&#41;](../mdx/tupletostr-mdx.md)|Retorna uma cadeia de caracteres formatada para MDX que corresponde a tupla especificada.|  
|[UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)|Retorna o nome exclusivo de uma dimensão, hierarquia, nível ou membro especificado.|  
|[UserName &#40;MDX&#41;](../mdx/username-mdx.md)|Retorna o nome de domínio e nome de usuário da conexão atual.|  
  
## <a name="subcube-functions"></a>Funções de subcubo  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Este &#40;MDX&#41;](../mdx/this-mdx.md)|Retorna o subcubo atual.|  
|[Deixa &#40;MDX&#41;](../mdx/leaves-mdx.md)|Retorna o conjunto de membros folha no membro, na dimensão ou na tupla especificada.|  
  
## <a name="tuple-functions"></a>funções de tupla  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Atual &#40;MDX&#41;](../mdx/current-mdx.md)|Retorna a tupla atual de um conjunto durante a iteração.|  
|[Item &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)|Retorna uma tupla de um conjunto.|  
|[Raiz &#40;MDX&#41;](../mdx/root-mdx.md)|Retorna uma tupla que consiste o **todos os** membros de cada hierarquia de atributo em um cubo, dimensão ou tupla.|  
|[StrToTuple &#40;MDX&#41;](../mdx/strtotuple-mdx.md)|Retorna a tupla especificada por uma cadeia de caracteres formatada para MDX.|  
  
## <a name="other-functions"></a>Outras funções  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Erro &#40;MDX&#41;](../mdx/error-mdx.md)|Identifica um erro, fornecendo uma mensagem de erro específica (opcional).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da linguagem MDX &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
