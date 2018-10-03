---
title: Suporte para propriedades XMLA (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7898c0f7263bf5355934ec072511bfd8483028
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215916"
---
# <a name="supported-xmla-properties-xmla"></a>Propriedades XMLA suportadas (XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a propriedades listadas na tabela a seguir. Você usa estas propriedades listadas na [propriedades](properties-element-xmla.md) elemento da [Discover](../xml-elements-methods-discover.md) e [Execute](../xml-elements-methods-execute.md) métodos.  
  
|Nome|Elemento|  
|----------|-------------|  
|AxisFormat|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Determina o formato usado dentro de um [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) para descrever os eixos do conjunto de dados multidimensional do conjunto de resultados. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*ClusterFormat*|O `MDDataSet` eixo é composto de um ou mais [CrossProduct](crossproduct-element-xmla.md) elementos.|  
|*CustomFormat*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa o *TupleFormat* formato desta configuração.|  
|*TupleFormat*|(Padrão) O `MDDataSet` eixo contém um ou mais [tupla](tuple-element-xmla.md) elementos.|  
  
 Esta propriedade pode ser usada com o método `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|BeginRange|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Contém um valor inteiro baseado em zero que corresponde a um valor de atributo `CellOrdinal`. (O `CellOrdinal` atributo faz parte do [célula](cell-element-mddataset-xmla.md) elemento no [CellData](celldata-element-xmla.md) seção `MDDataSet`.)<br /><br /> Usada junto com a propriedade `EndRange`, o aplicativo cliente pode usar essa propriedade a limitar um conjunto de dados OLAP retornado por um comando a um intervalo de células específico. Se –1 for especificado, serão retornadas todas as células até a célula especificada na propriedade `EndRange`.<br /><br /> O valor padrão desta propriedade é -1.<br /><br /> Esta propriedade pode ser usada com o método `Execute`.|  
|Catálogo|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Ao estabelecer uma sessão com uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para enviar um comando XMLA, essa propriedade é equivalente à propriedade OLE DB DBPROP_INIT_CATALOG.<br /><br /> Quando você define essa propriedade durante uma sessão para alterar o banco de dados atual da sessão, essa propriedade é equivalente à propriedade OLE DB DBPROP_CURRENTCATALOG.<br /><br /> O valor padrão desta propriedade é uma cadeia de caracteres vazia.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|CatalogLocation|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_CATALOGLOCATION.<br /><br /> O valor padrão desta propriedade é zero (0), equivalente a DBPROPVAL_CL_START.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|ClientProcessID|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Contém o identificador (ID) do thread de processo da sessão atual.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|CommitTimeout|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina quanto tempo, em segundos, a fase de confirmação de um XMLA comando que está sendo executado no momento espera antes da reversão. A fase de confirmação corresponde a comandos XMLA, como [instrução](../xml-elements-commands/statement-element-xmla.md) ou [processo](../xml-elements-commands/process-element-xmla.md).<br /><br /> Um valor de zero (0) indica que a instância espera indefinidamente.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|Conteúdo|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Determina o tipo de dados retornado dos métodos `Discover` e `Execute`. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Permite verificar a estrutura do comando, mas não a execução.|  
|*Esquema*|Retorna o esquema XML relacionado ao comando solicitado. O esquema de XML indica colunas e outras informações.|  
|*Dados*|Retorna somente os dados solicitados.|  
|*SchemaData*|(Padrão) Retorna a informações de esquema e os dados.|  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|Cube|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Contém o nome do cubo que define o contexto do comando. Se o próprio comando contém um nome de cubo, como dentro da cláusula FROM de uma expressões multidimensionais (MDX) [selecionar](/sql/mdx/mdx-data-manipulation-select) instrução, a configuração dessa propriedade será ignorada.<br /><br /> O valor padrão desta propriedade é uma cadeia de caracteres vazia.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DataSourceInfo|*Uso*<br /> Propriedade `String` necessária, de leitura/gravação<br /><br /> *Description*<br /> Contém as informações necessárias para estabelecer uma conexão à fonte de dados, por exemplo, o nome de instância.<br /><br /> Aplicativos clientes não devem construir o conteúdo da propriedade `DataSourceInfo` para enviar a uma instância. Em vez disso, o aplicativo cliente deve localizar as fontes de dados com suporte pelo provedor usando o `Discover` método para recuperar o [DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md) conjunto de linhas. O aplicativo cliente envia o mesmo valor da propriedade `DataSourceInfo` que o cliente recuperou do conjunto de linhas DISCOVER_DATASOURCES.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropCatalogTerm|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_CATALOGTERM.<br /><br /> O valor padrão para esta propriedade é "Database".<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropCatalogUsage|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_CATALOGUSAGE.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropColumnDefinition|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_COLUMNDEFINITION.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropConcatNullBehavior|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_CONCATNULLBEHAVIOR.<br /><br /> O valor padrão para esta propriedade é 1, equivalente a DBPROPVAL_CB_NULL.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropDataSourceReadOnly|*Uso*<br /> Opcional, somente leitura `Boolean` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_DATASOURCEREADONLY.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropGroupBy|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_GROUPBY.<br /><br /> O valor padrão para esta propriedade é 2, equivalente a DBPROPVAL_GB_EQUALS_SELECT.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropHeterogeneousTables|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_HETEROGENEOUSTABLES.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropIdentifierCase|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_IDENTIFIERCASE.<br /><br /> O valor padrão para esta propriedade é 8, equivalente a DBPROPVAL_IC_MIXED.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropInitMode|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_INIT_MODE.<br /><br /> Os únicos valores com suporte para esta propriedade são DB_MODE_READWRITE e DB_MODE_READ.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMaxIndexSize|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MAXINDEXSIZE.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMaxOpenChapters|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MAXOPENCHAPTERS.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMaxRowSize|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MAXROWSIZE.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMaxRowSizeIncludeBlob|*Uso*<br /> Propriedade `Boolean` opcional, somente leitura<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MAXROWSIZEINCLUDESBLOB.<br /><br /> O valor padrão desta propriedade é TRUE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMaxTablesInSelect|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MAXTABLESINSELECT.<br /><br /> O valor padrão desta propriedade é 1.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdAutoexists|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina o comportamento de autoexists. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0*|Valor padrão, igual a 1.|  
|*1*|Aplique deep autoexists a eixos de consulta e conjuntos nomeados. Inclui cláusulas e subseleções WHERE.|  
|*2*|Aplique deep autoexists a eixos de consulta e exclua conjuntos nomeados de autoexists. Inclui cláusulas e subseleções WHERE.|  
|*3*|Não aplique nenhum autoexists a conjuntos nomeados com a cláusula WHERE. Aplique shallow autoexists a eixos de consulta com a cláusula WHERE. Aplique deep autoexists a eixos de consulta e conjuntos nomeados com subseleções.|  
  
 Zero ou vazio são os valores padrão dessa propriedade. Esta é uma propriedade de sessão que só pode ser definida quando a sessão é criada.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdCacheMode|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdCachePolicy|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdCacheRatio|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdCacheRatio2|*Uso*<br /> Opcional, leitura/gravação `Double` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|*Uso*<br /> Propriedade `Integer` opcional, leitura/gravação<br /><br /> *Description*<br /> Determina comparação de cadeia de caracteres com diferenciação entre maiúsculas e minúsculas e funcionalidade de ordem de classificação. Esta propriedade controla a forma como as comparações são feitas nos conjuntos de caracteres que não oferecem suporte a caracteres maiúsculos e minúsculos, como, por exemplo, katakana para japonês e Hindi. O valor desta propriedade é definido na primeira conexão do thread de processo e afeta todas as conexões subsequentes nesse thread de processo.<br /><br /> Use a tabela a seguir para determinar quais sinalizadores devem ser usados.|  
  
|Nome|Valor|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|A diferenciação entre maiúsculas e minúsculas é ignorada.|  
|Não aplicável|*0x00000002*|Comparação binária. Os caracteres são comparados com base no valor subjacente no conjunto de caracteres, não na ordem do alfabeto específico.|  
|NORM_IGNORENONSPACE|*0x00000010*|São ignorados caracteres sem-espaçamento.|  
|NORM_IGNORESYMBOLS|*0x00000100*|São ignorados símbolos.|  
|NORM_IGNOREKANATYPE|*0x00001000*|Nenhuma diferenciação é feita entre os caracteres hiragana e katakana. Quando comparados, caracteres hiragana e katakana correspondentes são considerados iguais.|  
|NORM_IGNOREWIDTH|*0x00010000*|Nenhuma diferenciação é feita entre as versões de um único byte e de dois bytes do mesmo caractere.|  
|SORT_STRINGSORT|*0x00100000*|A pontuação é tratada da mesma forma que os símbolos.|  
  
 Para obter mais informações sobre a comparação de cadeias de caracteres no OLE DB, pesquise "CompareString" na seção Platform SDK da Biblioteca MSDN.  
  
 Não há um valor padrão para esta propriedade.  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdCompareCaseSensitiveStringFlags|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina comparação de cadeia de caracteres sem diferenciação entre maiúsculas e minúsculas e funcionalidade de ordem de classificação. Esta propriedade controla a forma como as comparações são feitas nos conjuntos de caracteres que não oferecem suporte a caracteres maiúsculos e minúsculos, como, por exemplo, katakana para japonês e Hindi. O valor desta propriedade é definido na primeira conexão do thread de processo e afeta todas as conexões subsequentes nesse thread de processo.<br /><br /> Use a tabela a seguir para determinar quais sinalizadores devem ser usados.|  
  
|Nome|Valor|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|A diferenciação entre maiúsculas e minúsculas é ignorada.|  
|Não aplicável|*0x00000002*|Comparação binária. Os caracteres são comparados com base no valor subjacente no conjunto de caracteres, não na ordem do alfabeto específico.|  
|NORM_IGNORENONSPACE|*0x00000010*|São ignorados caracteres sem-espaçamento.|  
|NORM_IGNORESYMBOLS|*0x00000100*|São ignorados símbolos.|  
|NORM_IGNOREKANATYPE|*0x00001000*|Nenhuma diferenciação é feita entre os caracteres hiragana e katakana. Quando comparados, caracteres hiragana e katakana correspondentes são considerados iguais.|  
|NORM_IGNOREWIDTH|*0x00010000*|Nenhuma diferenciação é feita entre as versões de um único byte e de dois bytes do mesmo caractere.|  
|SORT_STRINGSORT|*0x00100000*|A pontuação é tratada da mesma forma que os símbolos.|  
  
 Para obter mais informações sobre a comparação de cadeias de caracteres no OLE DB, pesquise "CompareString" na seção Platform SDK da Biblioteca MSDN.  
  
 Não há um valor padrão para esta propriedade.  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdDebugMode|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdDynamicDebugLimit|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdFlattened2|*Uso*<br /> Opcional, leitura/gravação `Boolean` propriedade<br /><br /> *Description*<br /> Executa saídas de todos os membros como uma hierarquia pai-filho em uma única coluna da tabela no resultado simplificado, exceto se a hierarquia pai-filho for solicitada no Eixo 0. O modelo Nível para colunas de saída não é usado.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdMDXCompatibility|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina como são tratados membros de espaços reservados em uma hierarquia imperfeita ou desbalanceada. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0*|Para compatibilidade com versões anteriores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], este valor é equivalente a 1|  
|*1*|Hierarquias em dimensões com função múltipla recebem uma legenda que inclui o nome da dimensão e o nome de hierarquia. A legenda tem o seguinte formato:<br /><br /> [Dimension].[Hierarchy]<br /><br /> Membros de espaço reservado são expostos.|  
|*2*|Hierarquias em dimensões com função múltipla recebem uma legenda que inclui o nome da dimensão e o nome de hierarquia. A legenda tem o seguinte formato:<br /><br /> [Dimension].[Hierarchy]<br /><br /> Membros de espaço reservado não são expostos.|  
|*3*|(Padrão) Membros de espaço reservado não são expostos.|  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdMDXUniqueNameStyle|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina o algoritmo para a geração dos nomes exclusivos de membros em uma dimensão. Essa propriedade pode ter os valores listados na tabela a seguir.<br /><br /> O valor padrão desta propriedade é 6.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0*|Para compatibilidade com versões anteriores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], este valor é equivalente a 2.|  
|*1*|Usa um algoritmo de caminho de chaves:<br /><br /> [dim].&[key1].&[key2]|  
|*2*|Usa um algoritmo de caminho de nomes:<br /><br /> [dim].[name1].&[name2]|  
|*3*|Usa nomes exclusivos garantidos que são estáveis com o passar do tempo.|  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdSQLCompatibility|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMsmdSubQueries|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Uma máscara de bits que determina o comportamento das subconsultas. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0*|Valor padrão, Compatível com versões anteriores do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Membros ou conjuntos calculados não são permitidos em subseleções ou subcubos.|  
|*1*|Membros ou conjuntos calculados são permitidos em subseleções ou subcubos. Não são incluídos ascendentes do membro calculado no espaço da subseleção ou subcubo.|  
|*2*|Membros ou conjuntos calculados são permitidos em subseleções ou subcubos. São incluídos ascendentes do membro calculado no espaço da subseleção ou subcubo.|  
  
 Zero ou vazio são os valores padrão dessa propriedade.  
  
 Esta é uma propriedade de sessão que só pode ser definida quando a sessão é criada.  
  
 Ver [membros calculados em subseleções e subcubos](../../multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) para obter uma explicação detalhada do comportamento de membros ou conjuntos calculados em subseleções e subcubos.  
  
|Nome|Elemento|  
|----------|-------------|  
|DbpropMsmdUseFormulaCache|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropMultiTableUpdate|*Uso*<br /> Opcional, somente leitura `Boolean` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MULTITABLEUPDATE.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropNullCollation|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_NULLCOLLATION.<br /><br /> O valor padrão desta propriedade é 4, equivalente a DBPROPVAL_NC_LOW.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropOrderByColumnsInSelect|*Uso*<br /> Opcional, somente leitura `Boolean` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_ORDERBYCOLUMNSINSELECT.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropOutputParameterAvailable|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_OUTPUTPARAMETERAVAILABILITY.<br /><br /> O valor padrão desta propriedade é 1, equivalente a DBPROPVAL_OA_NOTSUPPORTED.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropPersistentIdType|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_PERSISTENTIDTYPE.<br /><br /> O valor padrão desta propriedade é 4, equivalente a DBPROPVAL_PT_NAME.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropPrepareAbortBehavior|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_PREPAREABORTBEHAVIOR.<br /><br /> O valor padrão desta propriedade é 1, equivalente a DBPROPVAL_CB_DELETE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropPrepareCommitBehavior|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_PREPARECOMMITBEHAVIOR.<br /><br /> O valor padrão desta propriedade é 1, equivalente a DBPROPVAL_CB_DELETE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropProcedureTerm|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_PROCEDURETERM.<br /><br /> O valor padrão desta propriedade é "Membro calculado".<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropQuotedIdentifierCase|*Uso*<br /> Propriedade `Integer` opcional, somente leitura<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_QUOTEDIDENTIFIERCASE.<br /><br /> O valor padrão para esta propriedade é 8, equivalente a DBPROPVAL_IC_MIXED.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSchemaUsage|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_SCHEMAUSAGE.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSqlSupport|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_SQLSUPPORT.<br /><br /> O valor padrão desta propriedade é 512, equivalente a DBPROPVAL_SQL_SUBMINIMUM.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSubqueries|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_SUBQUERIES.<br /><br /> **Observação!** Embora Data Mining Extensions (DMX) aceite subconsultas, esta propriedade refere-se a suporte de subconsultas em SQL.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSupportedTxnDdl|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_SUPPORTEDTXNDDL.<br /><br /> O valor padrão desta propriedade é zero (0), equivalente a DBPROPVAL_TC_NONE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSupportedTxnIsoLevels|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_SUPPORTEDTXNISOLEVELS.<br /><br /> O valor padrão desta propriedade é 4096, equivalente a DBPROPVAL_TI_READCOMMITTED.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropSupportedTxnIsoRetain|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_SUPPORTEDTXNISORETAIN.<br /><br /> O valor padrão desta propriedade é 292, equivalente a uma combinação de DBPROPVAL_TR_ABORT_NO, DBPROPVAL_TR_COMMIT_NO e DBPROPVAL_TR_NONE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|DbpropTableTerm|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_TABLETERM.<br /><br /> O valor padrão para essa propriedade é "Cubo".<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|Dialect|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Estabelece o dialeto usado nas seguintes situações:<br /><br /> -O dialeto que o provedor usará a primeira vez em que o provedor tenta executar uma consulta.<br />-O dialeto usado para os erros de execução retornados como resultado de falhas de consulta.<br /><br /> Você pode usar a propriedade `Dialect` quando esperar que a maioria das consultas usará um dialeto específico sobre qualquer outro.<br /><br /> A sintaxe de consulta pode ser semelhante para dialetos de linguagem, como DMX e SQL. Como a sintaxe pode ser semelhante, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] talvez não consiga deduzir o dialeto da sintaxe de consulta. Se a consulta não for executada em um dialeto, a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode tentará executar a consulta novamente em um dialeto diferente.<br /><br /> Se a propriedade `Dialect` for definida, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará erros de execução de consulta no dialeto que tem precedência, mesmo se o provedor tentar executar a consulta novamente em outro dialeto. Por exemplo, a propriedade `Dialect` é definida como MDGUID_DM. Primeiro, o provedor tenta executar a consulta como uma consulta de mineração de dados, mas esta consulta falha. O provedor então reenvia a consulta como uma consulta de SQL. Porém, esta consulta de SQL também falha. Como o valor da propriedade `Dialect` é MDGUID_DM, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retorna uma mensagem de erro de mineração de dados, não uma mensagem de erro SQL.<br /><br /> Se a propriedade `Dialect` não for definida, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retornará erros de execução de consulta no último dialeto usado. Por exemplo, a propriedade `Dialect` não está definida, e uma consulta de mineração de dados falha. O provedor então reenvia a consulta como SQL. A consulta SQL também falha. Como a propriedade `Dialect` não está definida, o provedor retorna uma mensagem de erro SQL, em vez de uma mensagem de erro de mineração de dados.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> Os dialetos disponíveis para esta propriedade estão listados na tabela a seguir.|  
  
|Nome|Valor|Description|  
|----------|-----------|-----------------|  
|DBGUID_SQL|*C8B522D7-5CF3-11CE-ADE5-00AA0044773D*|O analisador SQL tem precedência.|  
|MDGUID_DM|*62C58FED-CCA5-44F1-83B6-7B45682B3904*|O analisador DMX tem precedência.|  
|MDGUID_MDX|*A07CCCD0-8148-11D0-87BB-00C04FC33942*|O analisador MDX tem precedência.|  
  
|Nome|Elemento|  
|----------|-------------|  
|Desabilitar fatos de pré-busca|*Uso*<br /> Propriedade `Boolean` opcional, leitura/gravação,<br /><br /> *Description*<br /> Quando definido como True, o mecanismo deixa de tentar pré-buscar valores para o comprimento da sessão.<br /><br /> O valor padrão desta propriedade é `False`.|  
|EffectiveRoles|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|EffectiveUserName|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Especifica o nome de uma conta a ser usada para anular o nome de usuário durante uma conexão a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O valor da propriedade não é normalizado, em que o MDX [nome de usuário](/sql/mdx/username-mdx) função retornará o valor literal se essa propriedade é usada. Esta propriedade só pode ser usada por administradores de servidor.<br /><br /> Esta propriedade aceita os seguintes tipos de SID: Usuário, Grupo, Alias, WellKnownGroup, Computador.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|EndRange|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Especifica um valor inteiro baseado em zero que corresponde a um valor de atributo `CellOrdinal`. (O `CellOrdinal` atributo faz parte do elemento `Cell` na seção `CellData` de `MDDataSet`).<br /><br /> Usada junto com a propriedade `BeginRange`, o aplicativo cliente pode usar essa propriedade a limitar um conjunto de dados OLAP retornado por um comando a um intervalo de células específico. Se –1 for especificado, serão retornadas todas as células da célula especificada na propriedade `BeginRange`.<br /><br /> O valor padrão desta propriedade é -1.<br /><br /> Esta propriedade pode ser usada com o método `Execute`.|  
|ExecutionMode|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> O valor padrão desta propriedade é *Execute*.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|ForceCommitTimeout|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina por quanto tempo, em segundos, a fase de confirmação de um comando XMLA que está sendo executado no momento espera antes de forçar a reversão de comandos emitidos anteriormente. A fase de confirmação corresponde a comandos XMLA, como `Statement` ou `Process`.<br /><br /> Um valor de zero (0) indica que a instância espera indefinidamente.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|Formato|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Determina o tipo de conjunto de resultados retornado dos métodos `Discover` e `Execute`. Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
 O valor padrão desta propriedade é *nativo*.  
  
 Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Tabular*|Retorna um conjunto de resultados usando o [conjunto de linhas](../xml-data-types/rowset-data-type-xmla.md) tipo de dados.|  
|*Multidimensional*|Retorna um conjunto de linhas usando o [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de dados.|  
|*nativo*|Nenhum formato é especificado explicitamente. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retorna o formato apropriado para o comando. O tipo de resultado real é identificado pelo namespace do resultado.|  
  
|Nome|Elemento|  
|----------|-------------|  
|ImpactAnalysis|*Uso*<br /> Opcional, somente gravação `Boolean` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|LocaleIdentifier|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Lê ou define o identificador de localidade (LCID) usado pelo método `Discover` ou `Execute`. Para obter a lista completa de hexadecimais de identificadores de idiomas, procure "Identificadores de idiomas", na Biblioteca MSDN<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MaximumRows|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropAggregateCellUpdate|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_AGGREGATECELL_UPDATE.<br /><br /> O valor padrão desta propriedade é 4, equivalente a MDPROPVAL_AU_SUPPORTED.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropAxes|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_AXES.<br /><br /> O valor padrão desta propriedade é 2147483647.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropDrillFunctions|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Determina o nível de suporte para funções de busca detalhada no servidor. Os valores a seguir são usados para compilar uma máscara de bits válida:<br /><br /> MDPROPVAL_MDF_BASIC (0x01)<br /><br /> MDPROPVAL_MDF_ASYMMETRIC (0x02)<br /><br /> MDPROPVAL_MDF_CALC_MEMBERS (0x04)<br /><br /> Os valores padrão são:<br /><br /> 3 para SQL Server 2008<br /><br /> 7 para SQL Server 2008 R2 e [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropFlatteningSupport|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_FLATTENING_SUPPORT.<br /><br /> O valor padrão desta propriedade é 1, equivalente a MDPROPVAL_FS_FULL_SUPPORT.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxCaseSupport|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_CASESUPPORT.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxDescFlags|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_DESCFLAGS.<br /><br /> O valor padrão desta propriedade é 7, equivalente a MDPROPVAL_MD_BEFORE, MDPROPVAL_MD_AFTER e MDPROPVAL_MD_SELF.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxFormulas|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_FORMULAS.<br /><br /> O valor padrão desta propriedade é 63, equivalente a uma combinação de MDPROPVAL_MF_WITH_CALCMEMBERS, MDPROPVAL_MF_WITH_NAMEDSETS, MDPROPVAL_MF_CREATE_CALCMEMBERS, MDPROPVAL_MF_CREATE_NAMEDSETS, MDPROPVAL_MF_SCOPE_SESSION e MDPROPVAL_MF_SCOPE_GLOBAL.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxJoinCubes|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_JOINCUBES.<br /><br /> O valor padrão desta propriedade é 1, equivalente a MDPROPVAL_MJC_SINGLECUBE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxMemberFunctions|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_MEMBER_FUNCTIONS.<br /><br /> O valor padrão desta propriedade é 15, equivalente a uma combinação de todos os valores OLE DB disponíveis.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxNamedSets|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Uma máscara de bits dos valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MNS_BASIC.|  
|*0x02*|MDPROPVAL_MNS_DYNAMIC.|  
|*0x04*|MDPROPVAL_MNS_DISPLAYFOLDER.|  
|*0x08*|MDPROPVAL_MNS_CAPTION.|  
  
 Um valor de 15 é o padrão para essa propriedade.  
  
|Nome|Elemento|  
|----------|-------------|  
|MdpropMdxNonMeasureExpressions|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_NONMEASURE_EXPRESSIONS.<br /><br /> O valor padrão desta propriedade é zero (0), equivalente a MDPROPVAL_NME_ALLDIMENSIONS.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxNumericFunctions|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_NUMERIC_FUNCTIONS.<br /><br /> O valor padrão desta propriedade é 2047, equivalente a uma combinação de MDPROPVAL_MNF_MEDIAN, MDPROPVAL_MNF_VAR, MDPROPVAL_MNF_STDDEV, MDPROPVAL_MNF_RANK, MDPROPVAL_MNF_AGGREGATE, MDPROPVAL_MNF_COVARIANCE, MDPROPVAL_MNF_CORRELATION, MDPROPVAL_MNF_LINREGSLOPE, MDPROPVAL_MNF_LINREGVARIANCE, MDPROPVAL_MNF_LINREG2 e MDPROPVAL_MNF_LINREGPOINT.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxObjQualification|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_OBJQUALIFICATION.<br /><br /> O valor padrão desta propriedade é 496, equivalente a uma combinação de MDPROPVAL_MOQ_DIM_HIER, MDPROPVAL_MOQ_DIMHIER_LEVEL, MDPROPVAL_MOQ_DIMHIER_MEMBER, MDPROPVAL_MOQ_LEVEL_MEMBER e MDPROPVAL_MOQ_MEMBER_MEMBER.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxOuterReference|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_OUTERREFERENCE.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxQueryByProperty|*Uso*<br /> Opcional, somente leitura `Boolean` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_QUERYBYPROPERTY.<br /><br /> O valor padrão desta propriedade é TRUE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxRangeRowset|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_RANGEROWSET.<br /><br /> O valor padrão desta propriedade é 4, equivalente a MDPROPVAL_RR_UPDATE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxSetFunctions|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_SET_FUNCTIONS.<br /><br /> O valor padrão desta propriedade é 524287, equivalente a uma combinação de MDPROPVAL_MSF_TOPPERCENT, MDPROPVAL_MSF_BOTTOMPERCENT, MDPROPVAL_MSF_TOPSUM, MDPROPVAL_MSF_BOTTOMSUM, MDPROPVAL_MSF_PERIODSTODATE, MDPROPVAL_MSF_LASTPERIODS, MDPROPVAL_MSF_YTD, MDPROPVAL_MSF_QTD, MDPROPVAL_MSF_MTD, MDPROPVAL_MSF_WTD, MDPROPVAL_MSF_DRILLDOWNMEMBER, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNMEMBERTOP, MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNLEVELTOP, MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM, MDPROPVAL_MSF_DRILLUPMEMBER, MDPROPVAL_MSF_DRILLUPLEVEL e MDPROPVAL_MSF_TOGGLEDRILLSTATE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxSlicer|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_SLICER.<br /><br /> O valor padrão desta propriedade é 2, equivalente a MDPROPVAL_MS_SINGLETUPLE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxStringCompop|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_MDX_STRING_COMPOP.<br /><br /> O valor padrão desta propriedade é 15, equivalente a uma combinação de MDPROPVAL_MSC_LESSTHAN, MDPROPVAL_MSC_GREATERTHAN, MDPROPVAL_MSC_LESSTHANEQUAL e MDPROPVAL_MSC_GREATERTHANEQUAL.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdpropMdxSubQueries|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> O valor 63 é o valor padrão para essa propriedade no SQL Server 2014.<br /><br /> O valor 31 é o valor padrão para essa propriedade no SQL Server 2008 R2 e no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> O valor 15 é o valor padrão para essa propriedade no SQL Server 2008.<br /><br /> Indica o nível de suporte das subconsultas em MDX. Uma máscara de bits dos valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MSQ_BASIC.|  
|*0x02*|MDPROPVAL_MSQ_ARBITRARYSHAPE.|  
|*0x04*|MDPROPVAL_MSQ_NONVISUAL.|  
|*0x08*|MDPROPVAL_MSQ_CALCMEMBERS.|  
  
|||  
|-|-|  
|*0x10*|MDPROPVAL_MSQ_CALCMEMBERS2|  
  
|Nome|Elemento|  
|----------|-------------|  
|MdpropNamedLevels|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_NAMED_LEVELS.<br /><br /> O valor padrão desta propriedade é 3, equivalente a uma combinação de MDPROPVAL_NL_NAMEDLEVELS e MDPROPVAL_NL_NUMBEREDLEVELS.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|MdxMissingMemberMode|*Uso*<br /> Opcional, somente gravação `String` propriedade<br /><br /> *Description*<br /> Indica se sentindo os membros ausentes são ignorados em instruções MDX.<br /><br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_MDX_MISSING_MEMBER_MODE.<br /><br /> O valor padrão desta propriedade é *padrão*.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*Default*|Usar valor gerado pela instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Erro*|Gerar um erro.|  
|*Ignorar*|Sempre ignorar membros ausentes.|  
  
|Nome|Elemento|  
|----------|-------------|  
|MDXSupport|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Especifica uma enumeração que descreve o grau de suporte de MDX.<br /><br /> `Value` = *Core* MDX todas as opções têm suporte.<br /><br /> Atualmente, é o único valor que contém a enumeração *Core*. Em versões futuras, serão definidos outros valores para esta enumeração.<br /><br /> O valor padrão desta propriedade é *Core*.<br /><br /> Esta propriedade pode ser usada com o método `Discover`.|  
|NonEmptyThreshold|*Uso*<br /> Propriedade `Integer` opcional, leitura/gravação<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|Senha|**Não há suporte para essa propriedade.**<br /><br /> *Uso*<br /> Propriedade `String` opcional, somente gravação<br /><br /> *Description*<br /> Para compatibilidade com versões anteriores, esta propriedade é ignorada sem gerar um erro quando usada com o método `Execute` ou `Discover`.|  
|ProviderName|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_DBMSNAME.<br /><br /> O valor padrão desta propriedade é "OLAP Server".<br /><br /> Esta propriedade pode ser usada com o método `Discover`.|  
|ProviderType|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_DATASOURCE_TYPE.<br /><br /> O valor padrão desta propriedade é 6.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|ProviderVersion|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB DBPROP_DBMSVER.<br /><br /> O valor padrão para esta propriedade é a versão da instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Esta propriedade pode ser usada com o método `Discover`.|  
|ReadOnlySession|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|RealTimeOlap|*Uso*<br /> Opcional, leitura/gravação `Boolean` propriedade<br /><br /> *Description*<br /> Quando definida como TRUE, indica que todas as partições que estão escutando notificações de tabelas devem ser consultadas em tempo real, ignorando o cache. Esta propriedade é equivalente à propriedade OLE DB DBPROP_MSMD_REAL_TIME_OLAP.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|ReturnCellProperties|*Uso*<br /> Opcional, leitura/gravação `Boolean` propriedade<br /><br /> *Description*<br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|Funções|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Especifica uma cadeia de caracteres delimitada por vírgula dos nomes de função com o qual um aplicativo cliente se conecta a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Esta propriedade permite que o usuário se conecte usando uma função diferente daquela que ele está usando no momento. Por exemplo, um administrador de servidor pode se conectar a um cubo como um membro de uma função para testar as permissões concedidas a essa função. Esse usuário deve ser um membro da função especificada para se conectar usando esta propriedade.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> **Observação!** Nomes de função diferenciam maiusculas de minúsculas. **Não use** espaços entre os nomes de funções delimitada por vírgula. Caso contrário, erros e resultados inesperados podem ser voltados por consultas a conjuntos de células protegidos.|  
|SafetyOptions|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Determina se bibliotecas não seguras podem ser registradas e carregadas por aplicativos cliente.<br /><br /> O valor desta propriedade também determina se a palavra-chave PASSTHROUGH é permitida em cubos locais. Ocorre um erro nas situações seguintes:<br /><br /> -Se um aplicativo cliente tenta criar um cubo local com uma instrução INSERT INTO que contenha a palavra-chave PASSTHROUGH.<br />-Se um aplicativo cliente tenta atualizar um cubo local que contém uma instrução INSERT INTO que usa a palavra-chave PASSTHROUGH.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Nome|Valor|Description|  
|----------|-----------|-----------------|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT|*0*|Este valor é tratado como DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE.<br /><br /> Para conexões a um cubo local, este valor depende se propriedade de cadeia de conexão CREATECUBE é usada. Se a propriedade da cadeia de conexão CREATECUBE é usada, este valor é igual a DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL. Caso contrário, este valor é igual a DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL|*1*|Este valor ativa todas as bibliotecas de função definida pelo usuário sem verificar se eles estão seguros para inicialização e scripting. Para conexões a cubos locais, esse valor permite o uso de procedimentos armazenados e da palavra-chave PASSTHROUGH em instruções INSERT INTO.<br /><br /> **Não recomendamos essa opção**.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE|*2*|Este valor ativa verifica se todas as classes de uma biblioteca específica de função definida pelo usuário estão marcadas para certificar-se de que elas estejam seguras para inicialização e scripting. Para conexões a cubos locais, esse valor impede o uso da palavra-chave PASSTHROUGH em instruções INSERT INTO e de procedimentos armazenados onde a propriedade PermissionSet não está definida como Segura.<br /><br /> Esse valor também remove ações na [MDSCHEMA_ACTIONS](../../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) de linhas de esquema que tem um valor de HTML ou comando na coluna ACTION_TYPE ou ter um valor de URL na coluna ACTION_TYPE e um valor na coluna CONTENT que não tem Comece com "http://" ou "https://".|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE|*3*|Este valor impede que funções definidas pelo usuário sejam usadas durante a sessão. Para conexões a cubos locais, esse valor impede o uso de todos procedimentos armazenados e da palavra-chave PASSTHROUGH em instruções INSERT INTO.<br /><br /> Este valor também remove todas as ações no conjunto de linhas de esquema MDSCHEMA_ACTIONS.|  
  
|Nome|Elemento|  
|----------|-------------|  
|SecuredCellValue|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Especifica o código de erro e os valores das propriedades de células `Value` e `Formatted Value` a serem retornados quando tentar acessar uma célula segura.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*0*|(Padrão) Para compatibilidade com versões anteriores, esse valor é igual a *1*. O significado deste valor padrão está sujeito a alteração em versões futuras.|  
|*1*|Retorna: HRESULT = NO_ERROR<br /><br /> A propriedade `Value` da célula contém o resultado como um tipo de dados variante. A cadeia de caracteres "#N/A" é retornada na propriedade `Formatted Value`.|  
|*2*|Retorna um erro como o valor de HRESULT.|  
|*3*|Retorna NULL nas propriedades `Value` e `Formatted Value`.|  
|*4*|Retorna um zero numérico (0) na propriedade `Value` e retorna um zero formatado na propriedade `Formatted Value`. Por exemplo, 0,00 é retornado na propriedade `Formatted Value` para uma célula cuja propriedade `Format` seja "#. ##."|  
|*5*|Retorna a cadeia de caracteres "#SEC" nas propriedades `Value` e `Formatted Value`.|  
  
|Nome|Elemento|  
|----------|-------------|  
|ServerName|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB, DBPROP_SERVERNAME.<br /><br /> O valor padrão desta propriedade é o nome da instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|ShowHiddenCubes|*Uso*<br /> Opcional, leitura/gravação `Boolean` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> O valor padrão desta propriedade é FALSE.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|SQLQueryMode|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Determina se cálculos são incluídos em consultas SQL.<br /><br /> O valor padrão desta propriedade é *Calculated*.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.<br /><br /> Essa propriedade pode ter os valores listados na tabela a seguir.|  
  
|Valor|Description|  
|-----------|-----------------|  
|*Dados*|Nenhum cálculo é incluído.|  
|*Calculado*|São retornados cálculos.|  
|*IncludeEmpty*|São retornados cálculos e linhas vazias.|  
  
|Nome|Elemento|  
|----------|-------------|  
|SQLSupport|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> O valor padrão desta propriedade é 512.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|SspropInitAppName|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Contém o nome do aplicativo cliente.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|SspropInitPacketsize|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Contém a ID do aplicativo cliente.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|SspropInitWsid|*Uso*<br /> Opcional, leitura/gravação `String` propriedade<br /><br /> *Description*<br /> Contém a ID da estação de trabalho cliente.<br /><br /> Não há um valor padrão para esta propriedade.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|StateSupport|*Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Especifica o grau de suporte para a capacidade de manutenção de status do processo.<br /><br /> *None* = <br />                        Não há suporte para a capacidade de manutenção de status do processo.<br /><br /> *Sessões* = Statefulness é fornecido por meio do suporte de sessão.<br /><br /> Para obter mais informações sobre o suporte de sessão e statefulness, consulte [Gerenciando conexões e sessões &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).<br /><br /> O valor padrão desta propriedade é *sessões*.<br /><br /> Esta propriedade pode ser usada com o método `Discover`.|  
|Tempo Limite|*Uso*<br /> Opcional, leitura/gravação `Integer` propriedade<br /><br /> *Description*<br /> Especifica o tempo máximo, em segundos, que a instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] deve esperar para que uma solicitação seja bem-sucedida antes de retornar um erro. Esta propriedade também determina o tempo máximo que a instância deve esperar para que uma atualização em uma tabela de write-back seja bem-sucedida antes de retornar um erro; equivalente à propriedade de cadeia de conexão Writeback Timeout.<br /><br /> O valor padrão desta propriedade é zero (0).<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|TransactionDDL|*Uso*<br /> Opcional, somente leitura `Integer` propriedade<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> O valor padrão desta propriedade é 0.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
|UserName|Esta propriedade não é mais suportada.<br /><br /> *Uso*<br /> Opcional, somente leitura `String` propriedade<br /><br /> *Description*<br /> Especifica uma cadeia de caracteres que retorna o nome de usuário que a instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] associa ao comando. Para compatibilidade com versões anteriores, esta propriedade é ignorada sem gerar um erro quando usada com o método `Execute` ou `Discover`. Esta propriedade é equivalente à propriedade OLE DB DBPROP_USERNAME.<br /><br /> O valor padrão desta propriedade é o nome de usuário que abriu a sessão ou conexão atual.<br /><br /> Esta propriedade pode ser usada com o método `Execute`.|  
|VisualMode|*Uso*<br /> Opcional, somente gravação `Integer` propriedade<br /><br /> *Description*<br /> Esta propriedade é equivalente à propriedade OLE DB MDPROP_VISUALMODE.<br /><br /> O valor padrão desta propriedade é zero (0), equivalente a DBPROPVAL_VISUAL_MODE_DEFAULT.<br /><br /> Esta propriedade pode ser usada com os métodos `Discover` e `Execute`.|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento PropertyList &#40;XMLA&#41;](propertylist-element-xmla.md)  
  
  
