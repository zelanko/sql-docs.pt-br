---
title: Fontes de dados e associações (SSAS Multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60b3e29ae94c4dcf5d136bcc01bf291a9a6118fe
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510542"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>Fontes de dados e associações (SSAS multidimensional)
  Podem ser acoplados cubos, dimensões e outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a uma fonte de dados. Uma fonte de dados pode ser um dos seguintes objetos:  
  
-   Uma fonte de dados relacional.  
  
-   Um pipeline do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que produz um conjunto de linhas (ou conjuntos de linhas em capítulos).  
  
 Os meios de expressão de uma fonte de dados variam de acordo com o tipo de fonte de dados. Por exemplo, uma fonte de dados relacional é diferenciada pela cadeia de caracteres de conexão. Para obter mais informações sobre fontes dados, consulte [Data Sources in Multidimensional Models](data-sources-in-multidimensional-models.md).  
  
 Independentemente da fonte de dados usada, a exibição de fonte de dados (DSV) contém os metadados da fonte de dados. Portanto, as associações de um cubo ou outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são expressas como associações ao DSV. Essas associações podem incluir associações a objetos de objetos lógicos, como exibições, colunas calculadas e relações que não existem fisicamente na fonte de dados. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adiciona uma coluna calculada que encapsula a expressão para o DSV e, em seguida, associa a medida OLAP correspondente a essa coluna no DSV. Para obter mais informações sobre DSVs, consulte [Data Source Views in Multidimensional Models](data-source-views-in-multidimensional-models.md).  
  
 Cada objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é associado à fonte de dados em seu próprio modo. Além disso, as associações de dados desses objetos e a definição da fonte de dados podem ser fornecidas de forma incorporada com a definição do objeto databound (por exemplo, a dimensão) ou associações fora de linha, como conjunto separado de definições.  
  
## <a name="analysis-services-data-types"></a>Tipos de dados do Analysis Services  
 Os tipos de dados que são usado em associações devem corresponder aos tipos de dados suportados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os seguintes tipos de dados estão definidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|Tipo de dados do Analysis Services|Descrição|  
|---------------------------------|-----------------|  
|BigInt|Um inteiro de 64 bytes com sinal. Esse tipo de dados é mapeado para o tipo de dados Int64 no Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_I8 no OLE DB.|  
|Bool|Um valor booliano. Esse tipo de dados é mapeado para o tipo de dados Boolean no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_BOOL no OLE DB.|  
|CURRENCY|Um valor de moeda que varia de -263 (ou -922.337.203.685.477,5808) a 263-1 (ou +922.337.203.685.477,5807) com uma precisão a dez milésimos de uma unidade de moeda. Esse tipo de dados é mapeado para o tipo de dados Decimal no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_CY no OLE DB.|  
|data|Dados de data, armazenados como um número de ponto flutuante com precisão dupla. A parte inteira é o número de dias desde 30 de dezembro de 1899, enquanto a parte fracionária é uma fração de um dia. Esse tipo de dados é mapeado para o tipo de dados DateTime no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_DATE no OLE DB.|  
|Double|Um número de ponto flutuante de precisão dupla dentro do intervalo de -1,79E +308 a 1,79E +308. Esse tipo de dados é mapeado para o tipo de dados Double no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_R8 no OLE DB.|  
|Integer|Um inteiro de 32 bytes com sinal. Esse tipo de dados é mapeado para o tipo de dados Int32 no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_I4 no OLE DB.|  
|Single|Um número de ponto flutuante de precisão única dentro do intervalo de -3,40E +38 a 3,40E +38. Esse tipo de dados é mapeado para o tipo de dados Single no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_R4 no OLE DB.|  
|SmallInt|Um inteiro com sinal de 16 bits. Esse tipo de dados é mapeado para o tipo de dados Int16 no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_I2 no OLE DB.|  
|TinyInt|Um inteiro com sinal de 8 bits. Esse tipo de dados é mapeado para o tipo de dados SByte no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_I1 no OLE DB.<br /><br /> Observação: Se uma fonte de dados contiver campos do tipo de dados tinyint e a propriedade AutoIncrement for definida como True, eles serão convertidos em inteiros na exibição da fonte de dados.|  
|UnsignedBigInt|Um inteiro não assinado de 64 bits. Esse tipo de dados é mapeado para o tipo de dados UInt64 no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_UI8 no OLE DB.|  
|UnsignedInt|Um inteiro não assinado de 32 bits. Esse tipo de dados é mapeado para o tipo de dados UInt32 no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_UI4 no OLE DB.|  
|UnsignedSmallInt|Um inteiro sem sinal de 16 bits. Esse tipo de dados é mapeado para o tipo de dados UInt16 no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_UI2 no OLE DB.|  
|WChar|Um fluxo com terminação nula de caracteres Unicode. Esse tipo de dados é mapeado para o tipo de dados String no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o tipo de dados DBTYPE_WSTR no OLE DB.|  
  
 Todos os dados recebidos da fonte de dados são convertidos para o tipo do [!INCLUDE[ssAS](../../includes/ssas-md.md)] especificado na associação (normalmente durante o processamento). Ocorrerá um erro caso a conversão não possa ser executada (por exemplo, de String para Int). [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] define o tipo de dados na associação para aquele que melhor corresponda ao tipo de fonte na fonte de dados. Por exemplo, os tipos de SQL Date, DateTime, SmallDateTime, DateTime2, DateTimeOffset são mapeados para [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date e o tipo de SQL Time é mapeado para String.  
  
## <a name="bindings-for-dimensions"></a>Associações para dimensões  
 Cada atributo de uma dimensão é associado a uma coluna em um DSV. Todos os atributos de uma dimensão devem ser provenientes de uma única fonte de dados. Entretanto, os atributos podem ser associados a colunas em tabelas diferentes. As relações entre as tabelas estão definidas no DSV. No caso em que mais de um conjunto de relações existe para a mesma tabela, pode ser necessário introduzir uma consulta nomeada no DSV para atuar como uma tabela 'alias'. Expressões e filtros são definidos no DSV com o uso de cálculos e consultas nomeados.  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>Associações para MeasureGroups, medidas e partições  
 Cada grupo de medidas tem as seguintes associações padrão:  
  
-   O grupo de medidas está associado a uma tabela em um DSV (por exemplo, `MeasureGroup.Source`).  
  
-   Cada medida é associada a uma coluna nessa tabela (por exemplo, `Measure.ValueColumn.Source`).  
  
-   Cada dimensão de grupo de medidas tem um conjunto de *atributos de granularidade* que define a granularidade do grupo de medidas. Cada um desses atributos deve ser associado à coluna ou colunas na tabela de fatos que contém a chave do atributo. (Para obter mais informações sobre atributos de granularidade, consulte Atributos de granularidade MeasureGroup, mais adiante neste tópico.)  
  
 Essas associações padrão podem ser substituídas seletivamente por partições. Cada partição pode especificar uma fonte de dados, uma tabela, um nome de consulta ou uma expressão de filtro diferente. A estratégia de particionamento mais comum é substituir a tabela por partição, usando a mesma fonte de dados. Dentre as alternativas estão a aplicação de um filtro diferente por partição ou a alteração da fonte de dados.  
  
 A fonte de dados padrão deve ser definida no DSV fornecendo as informações de esquema e incluindo os detalhes de relações. Quaisquer tabelas ou consultas adicionais especificadas no nível da partição não precisam ser listadas no DSV, mas elas têm o mesmo esquema da tabela padrão definida para o grupo de medidas ou, pelo menos, precisam conter todas as colunas usadas pelas medidas ou atributos de granularidade. As associações detalhadas por medida e atributo de granularidade não podem ser substituídas no nível da partição e supõe-se que elas estejam nas mesmas colunas que as definidas pelo grupo de medidas. Portanto, se a partição usa uma fonte de dados que, de fato, tem um esquema diferente, a consulta `TableDefinition` definida para a partição deve resultar no mesmo esquema usado pelo grupo de medidas.  
  
### <a name="measuregroup-granularity-attributes"></a>Atributos de granularidade MeasureGroup  
 Quando a granularidade de um grupo de medidas corresponde à granularidade conhecida no banco de dados e há uma relação direta entre a tabela de fatos e a tabela de dimensões, o atributo de granularidade deve ser associado apenas à coluna ou às colunas de chave estrangeira apropriadas na tabela de fatos. Por exemplo, considere as seguintes tabelas de fatos e de dimensões:  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 Se você analisar por produto pedido, para Produto Pedido na função da dimensão Vendas, o atributo de granularidade do Produto poderá estar associado a Sales.OrderedProductID.  
  
 Porém, em algumas vezes, o `GranularityAttributes` pode não existir como colunas na tabela de fatos. Por exemplo, o `GranularityAttributes` pode não existir como colunas nas seguintes circunstâncias:  
  
-   A granularidade OLAP é mais espessa que a granularidade na fonte.  
  
-   Uma tabela intermediária interpõe-se entre a tabela de fatos e a tabela de dimensões.  
  
-   A chave de dimensão não é igual à chave primária na tabela de dimensões.  
  
 Em todos esses casos, o DSV deve ser definido de modo que GranularityAttributes exista na tabela de fatos. Por exemplo, pode ser apresentada uma consulta nomeada ou uma coluna calculada.  
  
 Por exemplo, nas mesmas tabelas de exemplo citadas acima, se a granularidade fosse por Categoria, seria apresentada uma exibição de Vendas.  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 Nesse caso, a Categoria GranularityAttribute está associada à SalesWithCategory.OrderedProductCategory.  
  
### <a name="migrating-from-decision-support-objects"></a>Migrando do DSO (Decision Support Objects)  
 O DSO 8.0 (Decision Support Objects) permite que as `PartitionMeasures` sejam associadas novamente. Portanto, a estratégia de migração nesses casos é criar a consulta apropriada.  
  
 Da mesma maneira, não é possível associar novamente os atributos de dimensão de uma partição, embora o DSO 8.0 permita essa nova associação. A estratégia de migração nesses casos é definir as consultas nomeadas necessárias no DSV de modo que as mesmas tabelas e colunas existam no DSV para a partição à medida que as tabelas e colunas sejam usadas para a dimensão. Esses casos podem exigir a adoção da migração simples, na qual a cláusula From/Join/Filter é mapeada para uma consulta nomeada simples em vez de um conjunto estruturado de tabelas relacionadas. Como o DSO 8.0 permite que as PartitionDimensions sejam reassociadas, mesmo se partição estiver usando a mesma fonte de dados, a migração também exigirá vários DSVs para a mesma fonte de dados.  
  
 No DSO 8.0, as associações correspondentes podem ser expressas de duas maneiras diferentes, dependendo se os esquemas otimizados foram aplicados, associando a chave primária na tabela de dimensões ou a chave estrangeira na tabela de fatos. Em ASSL, as duas formas diferentes não são diferenciadas.  
  
 A mesma abordagem das associações se aplica a uma partição usando uma fonte de dados que não contenha as tabelas de dimensões, pois a associação é feita com a coluna de chave estrangeira na tabela de fatos, não com a coluna de chave primária na tabela de dimensões.  
  
## <a name="bindings-for-mining-models"></a>Associações para modelos de mineração  
 Um modelo de mineração é relacional ou OLAP. As associações de dados para um modelo de mineração relacional são, consideravelmente, diferentes das associações para um modelo de mineração OLAP.  
  
### <a name="bindings-for-a-relational-mining-model"></a>Associações para modelos de mineração relacional  
 Um modelo de mineração relacional depende das relações definidas no DSV para resolver qualquer ambiguidade referente a quais colunas estão associadas às fontes de dados. Em um modelo de mineração relacional, as associações de dados seguem estas regras:  
  
-   Cada coluna de tabela não aninhada é associada a uma coluna na tabela da caixa ou a tabela relacionada à tabela da caixa (seguindo uma relação muitos para um ou um para um). O DSV define as relações entre as tabelas.  
  
-   Cada coluna da tabela aninhada está associada à tabela de fontes. As colunas de propriedade da coluna da tabela aninhada são associadas às colunas na tabela de fontes ou a tabela relacionada à tabela de fontes. (Novamente, a associação segue uma relação muitos para um ou um para um.) Os model bindings de mineração não fornecem o caminho de junção para a tabela aninhada. Em vez disso, as relações definidas no DSV fornecem essas informações.  
  
### <a name="bindings-for-an-olap-mining-model"></a>Associações para modelos de mineração OLAP  
 Os modelos de mineração OLAP não têm o equivalente de um DSV. Portanto, as associações de dados devem remover as ambiguidades entre colunas e fontes de dados. Por exemplo, um modelo de mineração pode ter base no cubo Vendas e as colunas podem basear-se em Qtd, Valor e Nome do Produto. Como alternativa, um modelo de mineração pode basear-se em Produto e as colunas podem em Nome do Produto, Cor do Produto e uma tabela aninhada com a Qtd. de Vendas.  
  
 Em um modelo de mineração OLAP, as associações de dados seguem estas regras:  
  
-   Cada coluna de tabela não aninhada está associada a uma medida no cubo, a um atributo em uma dimensão do cubo (especificando a `CubeDimension` para remover a ambiguidade no caso de funções de dimensão) ou a um atributo em uma dimensão.  
  
-   Cada coluna de tabela associada é associada a uma `CubeDimension`, ou seja, esse processo define como navegar de uma dimensão para um cubo relacionado ou (no caso menos comum de tabelas aninhadas) de um cubo para uma de suas dimensões.  
  
## <a name="out-of-line-bindings"></a>associações fora de linha  
 Associações fora de linhas permitem alterar as associações de dados existentes temporariamente para a duração de um comando. Associações fora de linha referem-se às associações incluídas em um comando e não persistentes. As associações fora de linha aplicam-se apenas enquanto o comando específico é executado. Por outro lado, as associações incorporadas estão contidas na definição de objeto ASSL e persistem com a definição de objeto dentro dos metadados do servidor.  
  
 O ASSL permite que as associações incorporadas sejam especificadas em um comando `Process`, caso não esteja em um lote ou em um comando `Batch`. Se as associações incorporadas forem especificadas no comando `Batch`, todas as associações especificadas no comando `Batch` criarão um novo contexto de associação no qual todos os comandos `Process` do lote serão executados. Esse novo contexto de associação incluirá objetos processados indiretamente devido ao comando `Process`.  
  
 Quando as associações incorporadas são especificadas em um comando, elas substituem as associações incorporadas contidas no DDL persistido para os objetos especificados. Esses objetos processados podem incluir o objeto diretamente nomeado no comando `Process` ou incluir outros objetos cujo processamento é automaticamente iniciado como parte do processamento.  
  
 As associações incorporadas são especificadas pela inclusão do objeto de coleção opcional `Bindings` com o comando de processamento. A coleção opcional `Bindings` contém os elementos a seguir.  
  
|Propriedade|Cardinalidade|Tipo|Descrição|  
|--------------|-----------------|----------|-----------------|  
|`Binding`|0-n|`Binding`|Fornece uma coleção de novas associações.|  
|`DataSource`|0-1|`DataSource`|Substitui `DataSource` do servidor que seria usado.|  
|`DataSourceView`|0-1|`DataSourceView`|Substitui o `DataSourceView` do<br /><br /> servidor que seria usado.|  
  
 Todos os elementos relacionados a associações incorporadas são opcionais. Para qualquer elemento não especificado, o ASSL usa a especificação contida no DDL do objeto persistido. A especificação de `DataSource` ou `DataSourceView` no comando `Process` é opcional. Se `DataSource` ou `DataSourceView` for especificado, eles não serão instanciados e não persistirão depois que o comando `Process` for concluído.  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>Definição do tipo de associação fora de linha  
 Dentro da coleção fora de linha `Bindings`, o ASSL permite uma coleção de associações de vários objetos, cada um deles uma `Binding`. Cada `Binding` possui uma referência de objeto estendida, que é similar a uma referência de objeto, mas pode se referir aos objetos menores (por exemplo, atributos de dimensão e atributos de grupo de medidas). Esse objeto assume a forma plana típica do `Object` elemento no `Process` comandos, exceto que o \< *objeto*>\<*/objeto*> as marcas não estão presentes.  
  
 Cada objeto para o qual a associação é especificada é identificado por um elemento XML do formulário \< *objeto*> ID (por exemplo, `DimensionID`). Depois de identificar o objeto de maneira mais específica possível com a forma \< *objeto*> ID, identifique o elemento para o qual a associação está sendo especificada, que geralmente é `Source`. Um caso comum a observar é que `Source` é uma propriedade no `DataItem`, que são associações de colunas em um atributo. Nesse caso, você não especifica a marca `DataItem`; em vez disso, você simplesmente especifica a propriedade `Source` como se estivesse diretamente na coluna a ser vinculada.  
  
 As `KeyColumns` são identificadas pela ordem na coleção `KeyColumns`. Não é possível especificar, por exemplo, apenas a primeira e a terceira colunas de um atributo, pois não há como indicar que a segunda coluna de chave deve ser ignorada. Todas as colunas de chave devem estar presentes na associação fora de linha de um atributo de dimensão.  
  
 As `Translations`, embora não tenham nenhuma ID, são identificadas semanticamente por seu idioma. Portanto, as `Translations` em uma `Binding` precisam incluir seu identificador de idioma.  
  
 Um elemento adicional permitido em uma `Binding` que não existe diretamente no DDL é o `ParentColumnID`, que é usado em tabelas aninhadas para mineração de dados. Nesse caso, é necessário identificar a coluna pai na tabela aninhada para a qual associação está sendo fornecida.  
  
  
