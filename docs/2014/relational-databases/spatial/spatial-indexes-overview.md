---
title: Visão geral de índices espaciais | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- spatial indexes [SQL Server]
ms.assetid: b1ae7b78-182a-459e-ab28-f743e43f8293
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 36406bd60b4204469aca3d20862020870a8832fe
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068386"
---
# <a name="spatial-indexes-overview"></a>Visão geral de índices espaciais
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a dados e índices espaciais. Um *índice espacial* é um tipo de índice estendido que permite indexar uma coluna espacial. Uma coluna espacial é uma coluna de uma tabela que contém tipo de dados espaciais, como `geometry` ou `geography`.

> [!IMPORTANT]
>  Para obter uma descrição detalhada e exemplos dos recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo recursos que afetam índices espaciais, baixe o white paper sobre [Novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).

##  <a name="about-spatial-indexes"></a><a name="about"></a> Sobre índices espaciais

###  <a name="decomposing-indexed-space-into-a-grid-hierarchy"></a><a name="decompose"></a> Decompondo espaço indexado em uma hierarquia de grade
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], índices espaciais são criados usando árvores B, o que significa que os índices devem representar os dados espaciais bidimensionais na ordem linear de árvores B. Portanto, antes de ler dados em um índice espacial, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implementa uma decomposição uniforme hierárquica do espaço. O processo de criação de índice *decompõe* o espaço em uma *hierarquia de grade*de quatro níveis. Esses níveis são chamados de *nível 1* (o nível superior), *nível 2*, *nível 3*e *nível 4*.

 Cada nível sucessivo decompõe ainda mais o nível acima dele, de forma que cada célula de nível superior contém uma grade completa no próximo nível. Em um determinado nível, todas as grades têm o mesmo número de células ao longo dos dois eixos (por exemplo, 4x4 ou 8x8) e as células são todas de um único tamanho.

 A ilustração a seguir mostra a decomposição da célula superior direita em cada nível da hierarquia de uma grade de 4x4. Na realidade, todas as células são decompostas dessa maneira. Assim, por exemplo, a decomposição de um espaço em quatro níveis de grades de 4x4 realmente produz um total de 65.536 células de quatro níveis.

 ![Quatro níveis de mosaico recursivo](../../database-engine/media/spndx-recursive-levels-telescoped.gif "Quatro níveis de mosaico recursivo")

> [!NOTE]
>  A decomposição de espaço para um índice espacial depende da unidade de medida usada pelos dados do aplicativo.

 As células da hierarquia de grade são numeradas de maneira linear usando uma variação da curva de preenchimento de espaço de Hilbert. No entanto, para fins ilustrativos, esta discussão usa uma numeração baseada em linhas, em vez da numeração realmente produzida pela curva de Hilbert. Na ilustração a seguir, vários polígonos que representam prédios e linhas que representam ruas já foram colocados em uma grade 4x4 de nível 1. As células de nível 1 são numeradas de 1 a 16, a partir da célula superior esquerda.

 ![Polígonos e linhas colocados em uma grade 4x4 de nível 1](../../database-engine/media/spndx-level-1-objects.gif "Polígonos e linhas colocados em uma grade 4 x 4 de nível 1")

#### <a name="grid-density"></a>Densidade da grade
 O número de células ao longo dos eixos de uma grade determina sua *densidade*: quanto maior o número, mais densa a grade. Por exemplo, uma grade de 8x8 (que produz 64 células) é mais densa do que uma grade de 4x4 (que produz 16 células). A densidade da grade é definida em uma base por nível.

 A instrução [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] dá suporte a uma cláusula GRIDS que permite especificar diferentes densidades de grade em diferentes níveis. A densidade da grade em um determinado nível é especificada com uma das palavras-chave a seguir.

|Palavra-chave|Configuração da grade|Número de células|
|-------------|------------------------|---------------------|
|LOW|4X4|16|
|MEDIUM|8X8|64|
|HIGH|16X16|256|

 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quando o nível de compatibilidade do banco de dados é definido como 100 ou abaixo, o padrão é MEDIUM em todos os níveis. Quando o nível de compatibilidade do banco de dados é definido como 110 ou acima, o padrão é um esquema de grade automática.

 Você pode controlar o processo de decomposição especificando densidades de grade não padrão. Por exemplo, densidades diferentes de grade em diferentes níveis podem ser úteis para ajuste fino de um índice com base no tamanho do espaço indexado e nos objetos na coluna espacial.

> [!NOTE]
>  As densidades de grade de um índice espacial são visíveis nas colunas level_1_grid, level_2_grid, level_3_grid, e level_4_grid da exibição de catálogo [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) quando o nível de compatibilidade do banco de dados é definido como 100 ou abaixo. As `GEOMETRY_AUTO_GRID` / `GEOGRAPHY_AUTO_GRID` Opções de esquema de mosaico não preenchem essas colunas. a exibição de catálogo sys. spatial_index_tessellations tem `NULL` valores para essas colunas quando as opções de grade automática são usadas.

###  <a name="tessellation"></a><a name="tessellation"></a> Mosaico
 Após a decomposição de um espaço indexado em uma hierarquia de grade, o índice espacial lê os dados da coluna espacial, linha a linha. Depois de ler os dados de um objeto espacial (ou instância), o índice espacial executa um *processo de mosaico* para esse objeto. O processo de mosaico ajusta o objeto na hierarquia da grade associando o objeto a um conjunto de células da grade tocadas por ele (*células tocadas*). Iniciando no nível 1 da hierarquia de grade, o processo de mosaico continua com *amplitude primeiro* em todo o nível. Potencialmente, o processo pode continuar por todos os quatro níveis, um nível de cada vez.

 A saída do processo de mosaico é um conjunto de células tocadas que são registradas no índice espacial do objeto. Consultando essas células registradas, o índice espacial pode localizar o objeto no espaço em relação a outros objetos na coluna espacial que também são armazenados no índice.

#### <a name="tessellation-rules"></a>Regras do mosaico
 Para limitar o número de células tocadas registradas para um objeto, o processo de mosaico aplica várias regras de mosaico. Essas regras determinam a profundidade do processo de mosaico e quais das células tocadas são registradas no índice espacial do objeto.

 Essas regras são as seguintes:

-   A regra de cobertura

     Se o objeto cobrir uma célula completamente, a célula será considerada *coberta* pelo objeto. Uma célula coberta é contada e não é incluída no mosaico. Essa regra se aplica a todos os níveis da hierarquia de grade. A regra de cobertura simplifica o processo de mosaico e reduz a quantidade de dados que um índice espacial registra.

-   A regra de células por objeto

     Essa regra impõe o *limite de células por objeto*, que determina o número máximo de células que podem ser contadas para cada objeto, exceto no nível 1. Em níveis inferiores, a regra de células por objeto controla a quantidade de informações que podem ser registradas sobre o objeto.

-   A regra de célula mais profunda

     A regra de célula mais profunda gera a melhor aproximação de um objeto registrando apenas as células mais inferiores que foram incluídas no mosaico do objeto. Células pai não contribuem com a contagem de células por objeto e não são registradas no índice.

 Estas regras de mosaico são aplicadas recursivamente em cada nível de grade. O restante desta seção descreve as regras de mosaico em mais detalhes.

#### <a name="covering-rule"></a>Regra de cobertura
 Se o objeto cobrir uma célula completamente, a célula será considerada *coberta* pelo objeto. Por exemplo, na ilustração a seguir, uma das células de segundo nível, 15.11, está completamente coberta pela parte do meio de um octógono.

 ![Otimização da cobertura](../../database-engine/media/spndx-opt-covering.gif "Otimização da cobertura")

 Uma célula coberta é contada e registrada no índice e não é mais incluída no mosaico.

#### <a name="cells-per-object-rule"></a>Regra de células por objeto
 A extensão do mosaico de cada objeto depende principalmente do *limite células por objeto* do índice espacial. Esse limite define o número máximo de células que o mosaico pode contar por objeto. No entanto, observe que a regra de células por objeto não é imposta para o nível 1, portanto esse limite pode ser excedido. Se a contagem de nível 1 atingir ou exceder o limite de células por objeto, nenhum mosaico adicional ocorrerá nos níveis inferiores.

 Desde que a contagem seja menor do que o limite de células por objeto, o processo de mosaico continua. Começando com a célula tocada de número inferior (por exemplo, a célula 15.6 na ilustração anterior), o processo testa cada célula para avaliar se deve contá-la ou incluí-la no mosaico. Se a inclusão de uma célula no mosaico exceder o limite de células por objeto, a célula será contada e não será incluída no mosaico. Caso contrário, a célula será incluída no mosaico e as células de nível inferior que são tocadas pelo objeto serão contadas. O processo de mosaico continua dessa maneira, em modo de amplitude, em todo o nível. Esse processo é repetido recursivamente para as grades de nível inferior das células incluídas no mosaico até que o limite seja atingido ou não existam mais células para contar.

 Por exemplo, considere a ilustração anterior que mostra um octógono que se ajusta completamente à célula 15 da grade de nível 1. Na figura, a célula 15 foi incluída no mosaico, dissecando o octógono em nove células de nível 2. Esta ilustração pressupõe que o limite de células por objeto é 9 ou maior. No entanto, se o limite de células por objeto fosse 8 ou menor, a célula 15 não seria incluída no mosaico e a apenas a célula 15 seria contada para o objeto.

 Por padrão, o limite de células por objeto é de 16, o que fornece uma troca satisfatória entre espaço e precisão para a maior parte dos índices espaciais. No entanto, a instrução [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] dá suporte a uma cláusula CELLS_PER_OBJECT `=` *n* que permite especificar um limite de células por objeto entre 1 e 8192, inclusive.

> [!NOTE]
>  A configuração **cells_per_object** de um índice espacial é visível na exibição de catálogo [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) .

#### <a name="deepest-cell-rule"></a>Regra de célula mais profunda
 A regra da célula mais profunda explora o fato de que cada célula de nível inferior pertence à célula acima dela: uma célula de nível 4 pertence a uma célula de nível 3, uma célula de nível 3 pertence a uma célula de nível 2 e uma célula de nível 2 pertence a uma célula de nível 1. Por exemplo, um objeto que pertence à célula 1.1.1.1 também pertence à célula 1.1.1, à célula 1.1 e à célula 1. O conhecimento de tais relações da hierarquia de células é incorporado ao processador de consultas. Portanto apenas as células de nível mais profundo precisam ser registradas no índice minimizando as informações que o índice precisa armazenar.

 Na ilustração seguinte, um polígono em forma de diamante relativamente pequeno é incluído no mosaico. O índice usa o limite de células por objeto padrão de 16 que não é atingido para esse objeto pequeno. Portanto, o mosaico continua descendo até o nível 4. O polígono reside nas células de nível 1 até as células de nível 3: 4, 4.4 e 4.4.10 e 4.4.14. Entretanto, usando a regra da célula mais profunda, o mosaico conta apenas doze células de nível 4: 4.4.10.13-15 e 4.4.14.1-3, 4.4.14.5-7 e 4.4.14.9-11.

 ![Otimização de célula mais profunda](../../database-engine/media/spndx-opt-deepest-cell.gif "Otimização de célula mais profunda")

###  <a name="tessellation-schemes"></a><a name="schemes"></a> Esquemas de mosaico
 O comportamento de um índice espacial depende parcialmente de seu *esquema de mosaico*. O esquema de mosaico é específico ao tipo de dados. No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], índices espaciais oferecem suporte a dois esquemas de mosaico:

-   *Mosaico de grade geométrica*, que é o esquema para o `geometry` tipo de dados.

-   *Mosaico de grade geography*, que se aplica a colunas do `geography` tipo de dados.

> [!NOTE]
>  A configuração **tessellation_scheme** de um índice espacial é visível na exibição de catálogo [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) .

#### <a name="geometry-grid-tessellation-scheme"></a>Esquema de mosaico de grade geométrica
 O mosaico GEOMETRY_AUTO_GRID é o esquema de mosaico padrão para o tipo de dados `geometry` no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e versões posteriores.  O mosaico GEOMETRY_GRID é o único esquema de mosaico disponível para tipos de dados geometry no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta seção discute aspectos do mosaico de grade geométrica que são relevantes para trabalhar com índices espaciais: métodos com suporte e caixas delimitadoras.

> [!NOTE]
>  Você pode especificar explicitamente esse esquema de mosaico usando a cláusula USING (GEOMETRY_AUTO_GRID/GEOMETRY_GRID) da instrução [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

##### <a name="the-bounding-box"></a>A caixa delimitadora
 Dados geométricos ocupam um plano que pode ser infinito. Porém, no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um índice espacial requer um espaço finito. Para estabelecer um espaço finito para decomposição, o esquema de mosaico de grade geométrica requer uma *caixa delimitadora*retangular. A caixa delimitadora é definida por quatro coordenadas, `(` _x-min_**,**_y-min_ `)` e `(` _x-Max_**,**_y-Max_ `)` , que são armazenadas como propriedades do índice espacial. Essas coordenadas representam o seguinte:

-   *x-min* é a coordenada X do canto inferior esquerdo da caixa delimitadora.

-   *y-min* é a coordenada y do canto inferior esquerdo.

-   *x-max* é a coordenada X do canto superior direito.

-   *y-max* é a coordenada y do canto superior direito.

> [!NOTE]
>  Essas coordenadas são especificadas pela cláusula BOUNDING_BOX da instrução [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

 As `(` coordenadas _x-min_**,**_y-min_ `)` e `(` _x-Max_**,**_y-Max_ `)` determinam o posicionamento e as dimensões da caixa delimitadora. O espaço fora da caixa delimitadora é tratado como uma única célula numerada como 0.

 O índice espacial decompõe o espaço dentro da caixa delimitadora. A grade de nível 1 da hierarquia de grade preenche a caixa delimitadora. Para colocar um objeto geométrico na hierarquia da grade, o índice espacial compara as coordenadas do objeto com as coordenadas da caixa delimitadora.

 A ilustração a seguir mostra os pontos definidos pelas `(` coordenadas _x-min_**,**_y-min_ `)` e `(` _x-Max_**,**_y-Max_ `)` da caixa delimitadora. O nível superior da hierarquia da grade é mostrado como uma grade de 4x4. Para fins ilustrativos, os níveis inferiores são omitidos. O espaço fora da caixa delimitadora é indicado por um zero (0). Observe que o objeto 'A' se estende parcialmente além da caixa e o objeto 'B' está completamente fora da caixa na célula 0.

 ![Caixa delimitadora mostrando coordenadas e a célula 0.](../../database-engine/media/spndx-bb-4x4-objects.gif "Caixa delimitadora mostrando coordenadas e a célula 0.")

 Uma caixa delimitadora corresponde a uma parte dos dados espaciais de um aplicativo. Se a caixa delimitadora do índice contém completamente os dados armazenados na coluna espacial ou apenas uma parte é responsabilidade do aplicativo. Apenas operações computadas em objetos que estão completamente dentro da caixa delimitadora se beneficiam do índice espacial. Portanto, para obter o máximo benefício de um índice espacial em uma coluna `geometry`, é necessário especificar uma caixa delimitadora que contenha todos ou a maior parte dos objetos.

> [!NOTE]
>  As densidades da grade de um índice espacial são visíveis nas colunas bounding_box_xmin, bounding_box_ymin, bounding_box_xmax e bounding_box_ymax da exibição dr catálogo [sys.spatial_index_tessellations](/sql/relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql) .

#### <a name="the-geography-grid-tessellation-scheme"></a>Esquema de mosaico de grade geográfica
 Este esquema de mosaico aplica-se apenas a uma coluna de `geography`. Esta seção resume os métodos que têm suporte do mosaico de grade geográfica e discute como o espaço geodésico é projetado em um plano que, em seguida, é decomposto em uma hierarquia de grade.

> [!NOTE]
>  Você pode especificar explicitamente esse esquema de mosaico usando a cláusula USING (GEOGRAPHY_AUTO_GRID/GEOGRAPHY_GRID) da instrução [CREATE SPATIAL INDEX](/sql/t-sql/statements/create-spatial-index-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

##### <a name="projection-of-the-geodetic-space-onto-a-plane"></a>Projeção do espaço geodésico em um plano
 Computações em instâncias (objetos) de `geography` tratam o espaço que contém os objetos como um elipsoide geodésico. Para decompor esse espaço, o esquema de mosaico de grade geográfica divide a superfície do elipsoide em seus hemisférios superior e inferior e executa as seguintes etapas:

1.  Projeta cada hemisfério sobre as facetas de uma pirâmide quadrilátera.

2.  Achata as duas pirâmides.

3.  Une as pirâmides achatadas para formar um plano não euclidiano.

 A ilustração a seguir mostra uma exibição esquemática do processo de decomposição de três etapas. Nas pirâmides, as linhas pontilhadas representam os limites das quatro facetas de cada pirâmide. As etapas 1 e 2 ilustram o elipsoide geodésico usando uma linha horizontal verde para representar a longitude equatorial e uma série de linhas verticais verdes para representar várias linhas longitudinais. A etapa 1 mostra as pirâmides sendo projetadas sobre os dois hemisférios. A etapa 2 mostra as pirâmides sendo achatadas. A etapa 3 ilustra as pirâmides achatadas após terem sido combinadas para formar um plano mostrando várias linhas longitudinais projetadas. Observe que essas linhas projetadas se tornam retas e variam em comprimento, dependendo de sua localização nas pirâmides.

 ![Projeção do elipsoide em um plano](../../database-engine/media/spndx-geodetic-projection.gif "Projeção do elipsoide em um plano")

 Depois do espaço ser projetado no plano, o plano é decomposto na hierarquia de grade de quatro níveis. Níveis diferentes podem usar diferentes densidades de grade. A ilustração a seguir mostra o plano depois de decomposto em uma grade 4x4 de nível 1. Para fins ilustrativos, os níveis inferiores da hierarquia da grade são omitidos. Na realidade, o plano é decomposto completamente em uma hierarquia de grade de quatro níveis. Após o término do processo de decomposição, os dados geográficos são lidos, linha por linha, na coluna de geografia, e o processo de mosaico é executado em cada objeto.

 ![Grade de geografia de nível 1](../../database-engine/media/spndx-geodetic-level1grid.gif "Grade de geografia de nível 1")

##  <a name="methods-supported-by-spatial-indexes"></a><a name="methods"></a>Métodos com suporte de índices espaciais

###  <a name="geometry-methods-supported-by-spatial-indexes"></a><a name="geometry"></a>Métodos Geometry com suporte de índices espaciais
 Índices espaciais dão suporte aos seguintes métodos geometry orientados por conjunto em determinadas condições: STContains(), STDistance(), STEquals(), STIntersects(), STOverlaps(), STTouches() e STWithin(). Para que tenham suporte em um índice espacial, esses métodos devem ser usados dentro da cláusula WHERE ou JOIN ON de uma consulta e ocorrer dentro de um predicado com o seguinte formato geral:

 *Geometry1*. *method_name*(*Geometry2*)*comparison_operator * * valid_number*

 Para retornar um resultado não nulo, *geometry1* e *geometry2* devem ter o mesmo [SRID (identificador de referência espacial)](../spatial/spatial-reference-identifiers-srids.md). Caso contrário, o método retorna NULL.

 Índices espaciais oferecem suporte aos seguintes formulários de predicado:

-   *geometry1*.[STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)(*geometry2*) = 1

-   *Geometry1*. *Número* de < de*Geometry2*(de [distância](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type))

-   *geometry1*.[STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)(*geometry2*) <= *number*

-   *geometry1*.[STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)(*geometry2*)= 1

-   *geometry1*.[STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)(*geometry2*)= 1

-   *geometry1.* [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type) *(geometry2) = 1*

-   *geometry1*.[STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)(*geometry2*) = 1

-   *geometry1*.[STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)(*geometry2*)= 1

###  <a name="geography-methods-supported-by-spatial-indexes"></a><a name="geography"></a>Métodos de Geografia com suporte de índices espaciais
 Em determinadas condições, índices espaciais dão suporte aos seguintes métodos de geografia orientados a conjunto: STIntersects(), STEquals() e STDistance(). Para que tenham suporte de um índice espacial, esses métodos devem ser usados dentro da cláusula WHERE de uma consulta e ocorrer dentro de um predicado do seguinte formulário geral:

 *geography1*. *method_name*(*geography2*)*comparison_operator * * valid_number*

 Para retornar um resultado não nulo, *geography1* e *geography2* devem ter o mesmo [SRID (Identificador de Referência Espacial)](../spatial/spatial-reference-identifiers-srids.md). Caso contrário, o método retorna NULL.

 Índices espaciais oferecem suporte aos seguintes formulários de predicado:

-   *geography1*.[STIntersects](/sql/t-sql/spatial-geography/stintersects-geography-data-type)(*geography2*)= 1

-   *geography1*.[STEquals](/sql/t-sql/spatial-geography/stequals-geography-data-type)(*geography2*)= 1

-   *geography1*. *Número* de < de*Geography2*(de [distância](/sql/t-sql/spatial-geography/stdistance-geography-data-type))

-   *geography1*.[STDistance](/sql/t-sql/spatial-geography/stdistance-geography-data-type)(*geography2*) <= *number*

### <a name="queries-that-use-spatial-indexes"></a>Consultas que usam um índices espaciais
 Os índices espaciais só têm suporte em consultas que incluem um operador espacial indexado na cláusula `WHERE`. Por exemplo, a seguinte sintaxe:

```
[spatial object].SpatialMethod([reference spatial object]) [ = | < ] [const literal or variable]
```

 O otimizador de consulta compreende a intercambialidade de operações espaciais (que `@a.STIntersects(@b) = @b.STInterestcs(@a)` ). Mas, o índice espacial não será usado se o início de uma comparação não contiver o operador espacial (por exemplo, `WHERE 1 = spatial op` não usará o índice espacial). Para usar o índice espacial, reescreva a comparação (por exemplo, `WHERE spatial op = 1`).

 Assim como em qualquer outro índice, quando um índice espacial tem suporte, o uso do índice espacial é escolhido com base em custo; então, talvez o otimizador de consulta não opte por usar o índice espacial, embora todos os requisitos para seu uso sejam atendidos. Use o plano de execução para verificar se o índice espacial foi usado e, se necessário, fornecer dicas de consulta para forçar um plano de consulta desejado.

 O tipo de consulta de vizinho mais próximo também dará suporte a índices espaciais, embora apenas se uma sintaxe de consulta específica for escrita. A sintaxe apropriada é:

```
SELECT TOP(K) [WITH TIES] * 
FROM <Table> AS T [WITH(INDEX(<SpatialIndex>))]
WHERE <SpatialColumn>.STDistance(@reference_object) IS NOT NULL
ORDER BY <SpatialColumn>.STDistance(@reference_object) [;]
```

## <a name="see-also"></a>Consulte Também
 [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)


