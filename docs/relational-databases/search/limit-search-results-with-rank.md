---
title: Limitar os resultados da pesquisa com RANK | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb7d238a3ff475fe47dbe652adab3cc49ca3a3b2
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973685"
---
# <a name="limit-search-results-with-rank"></a>Limite resultados de pesquisa com RANK
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  As funções [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) retornam uma coluna denominada RANK que contém valores ordinais de 0 a 1000 (valores de classificação). Esses valores são usados para classificar as linhas retornadas de acordo com o grau de correspondência com os critérios de seleção. Os valores de classificação indicam apenas uma ordem relativa de relevância das linhas no conjunto de resultados, sendo que um valor inferior indica menor relevância. Os valores reais não são importantes e geralmente são diferentes em cada execução da consulta.  
  
> [!NOTE]  
>  Os predicados CONTAINS e FREETEXT não retornam valores de classificação.  
  
 O número de itens que correspondem a uma condição de pesquisa geralmente é muito grande. Para impedir que as consultas CONTAINSTABLE ou FREETEXTTABLE retornem muitas correspondências, use o parâmetro *top_n_by_rank* opcional, que retorna apenas um subconjunto de linhas. *top_n_by_rank* é um valor inteiro, *n*, que especifica que somente as *n* correspondências com classificação mais alta sejam retornadas, em ordem decrescente. Se *top_n_by_rank* for combinado com outros parâmetros, a consulta retornará menos linhas do que o número de linhas que corresponde de fato a todos os predicados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ordena as correspondências por classificação e retorna somente o número especificado de linhas. Essa opção pode resultar em um aumento significativo no desempenho. Por exemplo, uma consulta que normalmente retornaria 100.000 linhas de uma tabela de um milhão de linhas será processada com muito mais rapidez se apenas as 100 primeiras linhas forem solicitadas.  
  
##  <a name="examples"></a> Exemplos do uso de RANK para limitar os resultados da pesquisa  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>Exemplo A: pesquisando apenas as três primeiras correspondências  
 O exemplo a seguir usa CONTAINSTABLE para retornar apenas as três primeiras correspondências.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>Exemplo B: pesquisando as dez primeiras correspondências  
 O exemplo a seguir usa CONTAINSTABLE para retornar a descrição dos 5 produtos principais onde a coluna `Description` contém a palavra "aluminum" próxima à palavra "light" ou "lightweight".  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> Como os resultados de consultas de pesquisa são classificados  
 A pesquisa de texto completo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode gerar uma pontuação (ou valor de classificação) opcional que indica a relevância dos dados retornados por uma consulta de texto completo. Este valor de classificação é calculado para cada linha e pode ser usado como critério de ordenação para classificar o conjunto de resultados de uma determinada consulta por relevância. Os valores de classificação indicam apenas uma ordem relativa de relevância das linhas do conjunto de resultados. Os valores reais não são importantes e geralmente são diferentes em cada execução da consulta. O valor de classificação não guarda nenhuma importância entre as consultas.  
  
### <a name="statistics-for-ranking"></a>Estatísticas para a classificação  
 Quando um índice é criado, as estatísticas são coletadas para serem usadas na classificação. O processo de construir um catálogo de texto completo não resulta diretamente em uma única estrutura de índice. Em vez disso, o Mecanismo de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria índices intermediários conforme os dados são indexados. O Mecanismo de Texto Completo então mescla esses índices em um índice maior, conforme necessário. Este processo pode ser repetido muitas vezes. Em seguida, o Mecanismo de Texto Completo conduz uma "mesclagem mestra" que combina todos os índices intermediários em um grande índice mestre.  
  
 As estatísticas são coletadas a cada nível de índice intermediário. As estatísticas são mescladas quando os índices são mesclados. Alguns valores estatísticos só podem ser gerados durante o processo de mesclagem mestra.  
  
 Ao classificar um conjunto de resultados da consulta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa estatísticas do índice intermediário maior. Isto depende se os índices intermediários foram mesclados ou não. Como resultado, as estatísticas de classificação poderão variar em precisão se os índices intermediários tiverem sido mesclados. Isto explica porque a mesma consulta pode retornar diferentes resultados de classificação no decorrer do tempo conforme os dados indexados do texto completo são adicionados, modificados e excluídos; e conforme os índices menores são mesclados.  
  
 Para minimizar o tamanho do índice e a complexidade computacional, as estatísticas são sempre arredondadas.  
  
 A lista a seguir inclui alguns termos usados comumente e os valores estatísticos que são importantes para a classificação.  
  
 Propriedade  
 Uma coluna indexada de texto completo da linha.  
  
 Document  
 A entidade retornada em consultas. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] isso corresponde a uma linha. Um documento pode ter diversas propriedades, assim como uma linha pode ter diversas colunas indexadas de texto completo.  
  
 Índice  
 Um único índice invertido de um ou mais documentos. Isto pode estar por inteiro na memória ou no disco. Muitas estatísticas de consulta são relativas ao índice individual onde a correspondência ocorreu.  
  
 Catálogo de texto completo  
 Uma coleção de índices intermediários tratada como uma entidade para consultas. Catálogos são a unidade de organização visível para o administrador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Palavra, token ou item  
 A unidade de correspondência no mecanismo de texto completo. Fluxos de texto de documentos são convertidos em palavras ou tokens por separadores de palavras de um determinado idioma.  
  
 Ocorrência  
 O deslocamento da palavra em uma propriedade de documento como determinado pelo separador de palavras. A primeira palavra está na ocorrência 1, a próxima na 2, e assim por diante. A fim de evitar falsos positivos em frase e consultas por proximidade, o término da oração e término do parágrafo introduz intervalos maiores de ocorrência.  
  
 TermFrequency  
 O número de vezes que o valor da chave ocorre em uma linha.  
  
 IndexedRowCount  
 Número total de linhas indexadas. Isto é computado com base nas contagens mantidas nos índices intermediários. Este número pode variar em precisão.  
  
 KeyRowCount  
 Total de linhas no catálogo de texto completo que contém uma dada chave.  
  
 MaxOccurrence  
 A maior ocorrência armazenada em um catálogo de texto completo a uma determinada propriedade em uma linha.  
  
 MaxQueryRank  
 A classificação máxima, 1000, retornada pelo Mecanismo de Texto Completo.  
  
  
### <a name="rank-computation-issues"></a>Problemas na computação da classificação  
 O processo de computação da classificação depende de vários fatores.  Separadores de palavra de idiomas diferentes convertem o texto em token de forma diferente. Por exemplo, a cadeia de caracteres “casa de cachorro” pode ser quebrada em “casa” “cachorro” por um separador de palavra e em “casa de cachorro” por outro separador de palavra. Isto significa que a correspondência e a classificação podem variar com base em um idioma específico, porque não só as palavras são diferentes como também o tamanho do documento. A diferença de tamanho do documento pode afetar a classificação para todas as consultas.  
  
 Estatísticas como **IndexRowCount** podem variar muito. Por exemplo, se um catálogo tem 2 bilhões de linhas no índice mestre, um novo documento será indexado no índice intermediário da memória, e a classificação daquele documento será com base no número de documentos no índice da memória que poderão ser inclinados quando comparados às classificações dos documentos do índice mestre. Por esta razão, recomenda-se que, após qualquer população que resulte em um grande número de linhas, os índices indexados ou reindexados sejam mesclados em um índice mestre usando a função ALTER FULLTEXT CATALOG... Instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] REORGANIZE. O Mecanismo de Texto Completo também mesclará automaticamente os índices com base em parâmetros como o número e o tamanho dos índices intermediários.  
  
 Os valores**MaxOccurrence** são normalizados em 1 de 32 intervalos. Isto significa, por exemplo, que um documento de 50 palavras é tratado da mesma forma que um documento de 100 palavras. Abaixo está a tabela usada para normalização. Como os tamanhos dos documentos estão no intervalo entre os valores 32 e 128 da tabela adjacente, eles são tratados como se tivessem o mesmo tamanho, 128 (32 < **docLength** <= 128).  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>Classificação do CONTAINSTABLE  
 A classificação[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) usa o seguinte algoritmo:  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 As correspondências de frase são classificadas exatamente como as chaves individuais, com exceção da **KeyRowCount** (o número de linhas contendo a frase) que é estimada e pode não ser precisa e ser maior do que o número real.  
  
 **Classificação de NEAR**  
  
 CONTAINSTABLE oferece suporte a consultas de dois ou mais termos de pesquisa próximos entre si usando a opção NEAR. O valor de classificação de cada linha retornada baseia-se em vários parâmetros. Um fator de classificação principal é o número total de correspondências (ou *ocorrências*) relativo ao tamanho do documento. Dessa forma, se, por exemplo, um documento de 100 palavras e um documento de 900 palavras contiverem correspondências idênticas, o documento de 100 palavras terá uma classificação mais alta.  
  
 O comprimento total de cada ocorrência em uma linha também contribuirá para a classificação dessa linha com base na distância entre o primeiro e o último termos de pesquisa daquela ocorrência. Quanto menor a distância, mais a ocorrência contribuirá para o valor de classificação da linha. Se uma consulta de texto completo não especificar um valor inteiro como a distância máxima, um documento que só contém ocorrências cujas distâncias são separadamente maiores que 100 condições lógicas, terá uma classificação de 0.  
  
 **Classificação de ISABOUT**  
  
 CONTAINSTABLE oferece suporte a consultas de termos ponderados usando a opção ISABOUT. ISABOUT é uma consulta do espaço de vetor na terminologia de recuperação de informações tradicionais. O algoritmo padrão de classificação usado é Jaccard, uma fórmula muito conhecida. A classificação é computada para cada termo da consulta e combinada conforme descrito abaixo.  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>Classificação de FREETEXTTABLE  
 A classificação de[FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) tem como base a fórmula de classificação OKAPI BM25. Consultas FREETEXTTABLE adicionarão palavras à consulta via geração por flexão (formas flexionadas das palavras originais da consulta); essas palavras são tratadas como palavras separadas, sem nenhuma relação especial com as palavras das quais foram geradas. Sinônimos gerados do recurso Thesaurus serão tratados como palavras separadas, em condições de igual equilíbrio. Cada palavra na consulta contribui para a classificação.  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N - R + r + 0.5 ) ) / ( ( R - r + 0.5 ) * ( n - r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 - b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)  
  
  
