---
title: Conjunto de linhas DISCOVER_CALC_DEPENDENCY | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86f0ed45ced35aba884f05284f886334d250694d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discovercalcdependency-rowset"></a>Conjunto de linhas DISCOVER_CALC_DEPENDENCY
  Cria relatórios sobre as dependências entre cálculos e sobre os objetos referenciados nesses cálculos. Você pode usar essas informações em um aplicativo cliente para gerar relatórios sobre problemas com fórmulas complexas ou para advertir quando objetos relacionados forem excluídos ou modificados. Você também pode usar o conjunto de linhas para extrair as expressões DAX usadas em medidas ou colunas calculadas.  
  
 **Aplica-se a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_CALC_DEPENDENCY** contém as colunas a seguir. A tabela também especifica o tipo de dados, indica se a coluna pode ser restrita para limitar as linhas que são retornadas e fornece uma descrição de cada coluna.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o nome de banco de dados que contém o objeto para o qual a análise de dependência é solicitada. Se ele for omitido, o banco de dados atual será usado.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_DEPENDENCY_CALC** usando esta coluna.|  
|**OBJECT_TYPE**|**DBTYPE_WSTR**|Sim|Indica o tipo do objeto para o qual análise de dependência é solicitada. O objeto deve ter um dos seguintes tipos:<br /><br /> **ACTIVE_RELATIONSHIP**: uma relação ativa<br /><br /> **CALC_COLUMN**: coluna calculada<br /><br /> **HIERARCHY**: uma hierarquia<br /><br /> **MEASURE**: uma medida<br /><br /> **RELATIONSHIP**: uma relação<br /><br /> **KPI**: um KPI (indicador chave de desempenho)<br /><br /> <br /><br /> Observe que o **DISCOVER_DEPENDENCY_CALC** linhas pode ser restringido usando esta coluna.|  
|**CONSULTA**|**DBTYPE_WSTR**|Sim|Para modelos tabulares criados no [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)], você pode incluir uma consulta ou expressão DAX para mostrar o gráfico de dependência para essa consulta ou expressão. A restrição QUERY fornece aplicativos cliente com uma maneira de determinar quais objetos são usados por uma consulta DAX.<br /><br /> A restrição **QUERY** pode ser especificada no XMLA ou na cláusula WHERE de uma consulta DMV. Consulte a seção de exemplos para obter mais informações.|  
|**TABELA**|**DBTYPE_WSTR**||O nome da tabela que contém o objeto para o qual as informações sobre dependência são geradas.|  
|**OBJETO**|**DBTYPE_WSTR**||O nome do objeto para o qual as informações de dependência são geradas. Se o objeto for uma medida ou coluna calculada, use o nome da medida. Se o objeto for uma relação, o nome da tabela (ou dimensão de cubo) que contém a coluna que participa da relação.|  
|**EXPRESSÃO**|**DBTYPE_WSTR**||A fórmula que contém o objeto para o qual são buscadas dependências.|  
|**REFERENCED_OBJECT_TYPE**|**DBTYPE_WSTR**||Retorna o tipo do objeto que tem uma dependência no objeto referenciado. Os objetos retornados podem ter os seguintes tipos:<br /><br /> **CALC_COLUMN**: uma coluna calculada<br /><br /> **COLUMN**: uma coluna de dados<br /><br /> **MEASURE**: uma medida<br /><br /> **RELATIONSHIP**: uma relação<br /><br /> **KPI**: um KPI (indicador chave de desempenho)|  
|**REFERENCED_TABLE**|**DBTYPE _ WSTR**||O nome da tabela que contém o objeto dependente.|  
|**REFERENCED_OBJECT**|**DBTYPE _ WSTR**||O nome do objeto que tem uma dependência no objeto referenciado. Para medidas e colunas calculadas, o nome da medida ou coluna. Para relações, o nome totalmente qualificado da tabela (ou dimensão de cubo) que contém o objeto dependente.|  
|**REFERENCED_EXPRESSION**|**DBTYPE_WSTR**||Uma fórmula, em uma coluna calculada ou em uma medida, que é dependente no objeto referenciado.|  
  
## <a name="example"></a>Exemplo  
 **Sintaxe básica**  
  
 A consulta a seguir é uma consulta DMV simples que retorna valores para todas as colunas neste conjunto de linhas, usando o banco de dados padrão na conexão atual. Você pode executar essa consulta em uma janela de consulta MDX e exibir seus resultados no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]. Você também pode seguir as técnicas descritas em [consultando DMVs do Power Pivot do Excel](http://go.microsoft.com/fwlink/?LinkID=235146) para exibir os resultados da consulta DMV no Excel.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>Exemplo  
 **Classificar os resultados**  
  
 Adicionar um ORDER BY para classificar o conjunto de linhas por tabela ou outra coluna.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>Exemplo  
 **Filtrar usando uma cláusula WHERE**  
  
 A próxima consulta mostra como adicionar uma restrição usando a cláusula WHERE. As colunas a seguir podem ser usadas como filtros de consulta em uma cláusula WHERE: **Database_Name**, **Object_Type**e **Query**.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>Exemplo  
 **Filtrar em medidas e colunas calculadas para exibir expressões DAX subjacentes.**  
  
 Nessa consulta, você pode selecionar apenas a medida ou coluna calculada e, em seguida, exibir a expressão DAX usada no cálculo. A coluna EXPRESSION contém as expressões DAX. Se você estiver usando DISCOVER_CALC_DEPENDENCY para extrair a expressão DAX usada no modelo, essa consulta será suficiente para essa finalidade. Ela retorna todas as expressões usadas no modelo, em ordem crescente.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>Exemplo  
 **Filtrar usando QUERY**  
  
 Usando a restrição QUERY, você pode fornecer uma consulta DAX para exibir todos os objetos usados na consulta. Considere uma consulta simples como 'Evaluate Customer'. Conforme foi escrito, essa consulta retorna linhas de dados do cliente, onde a composição da linha é baseada nas colunas na tabela Customer. Se você executar agora DISCOVER_CALC_DEPENDENCY com uma restrição QUERY de ‘Evaluate Customer’, obterá as colunas (ou objetos) usados na consulta. Nesse caso, é uma lista das colunas na tabela Customer.  
  
 O próximo conjunto de consultas demonstra sintaxe para a restrição QUERY. Você pode executar essas consultas no [Modelo Tabular do AdventureWorks SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) para exibir o conjunto de resultados.  
  
 A primeira consulta mostra como especificar uma restrição QUERY para nomes de objetos que incluem espaços. A segunda consulta, emprestada de [Executar consultas DAX por meio de OLE DB e ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=254329), é uma consulta mais complexa que inclui objetos de várias tabelas.  
  
> [!NOTE]  
>  Embora as consultas pareçam usar aspas duplas, de fato somente aspas simples são usadas. Um par de aspas simples envolve ' Evaluate \<Tablename >', e aspas simples usadas em torno do nome de tabela precisam ser substituídas por aspas duplas. Aspas simples em volta do nome da tabela são necessárias somente para os nomes de tabelas que incluem um espaço.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>Exemplo  
 **Exemplo de consulta XMLA de restrição**  
  
 Você pode usar um comando Discover do XMLA para retornar os objetos de consulta em uma tabela. O XMLA retorna resultados como XML bruto. Você pode usar ADOMD.NET para analisar os resultados em um formato mais legível.  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Usar dinâmico exibições de gerenciamento &#40; DMVs &#41; para monitorar o Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
