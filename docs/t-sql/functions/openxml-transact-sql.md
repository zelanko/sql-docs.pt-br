---
title: OPENXML (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs: TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7b1fb1d28c4bddb679bd4aab8ce6cb11f21caca5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML fornece uma exibição de conjunto de linhas em um documento XML. Como OPENXML é um provedor de conjunto de linhas, OPENROWSET pode ser usado em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] nas quais os provedores de conjunto de linhas, como uma tabela, exibição ou a função OPENROWSET, podem aparecer.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IDOC*  
 É o indentificador de documento da representação interna de um documento XML. A representação interna de um documento XML é criada chamando **sp_xml_preparedocument**.  
  
 *rowpattern*  
 É o padrão XPath usado para identificar os nós (no documento XML cujo identificador é passado a *idoc* parâmetro) a ser processado como linhas.  
  
 *sinalizadores*  
 Indica o mapeamento que deve ser usado entre os dados XML e o conjunto de linhas relacional, e como a coluna de derramamento deve ser preenchida. *sinalizadores de* é um parâmetro de entrada opcional e pode ser um dos valores a seguir.  
  
|Valor do byte|Description|  
|----------------|-----------------|  
|**0**|O padrão será a **centrado em atributo** mapeamento.|  
|**1**|Use o **centrado em atributo** mapeamento. Pode ser combinado com XML_ELEMENTS. Nesse caso, **centrado em atributo** mapeamento é aplicado primeiro e, em seguida, **centrado em elemento** mapeamento é aplicado a todas as colunas que ainda não são tratadas.|  
|**2**|Use o **centrado em elemento** mapeamento. Pode ser combinado com XML_ATTRIBUTES. Nesse caso, **centrado em atributo** mapeamento é aplicado primeiro e, em seguida, **centrado em elemento** mapeamento é aplicado a todas as colunas ainda não foram tratadas.|  
|**8**|Pode ser combinado (OR lógico) com XML_ATTRIBUTES ou XML_ELEMENTS. No contexto de recuperação, esse sinalizador indica que os dados consumidos não devem ser copiados para a propriedade de estouro  **@mp:xmltext** .|  
  
 *SchemaDeclaration*  
 É a definição de esquema do formulário: *ColName**ColType* [*ColPattern* | *metapropriedade*] [**,***ColNameColType* [*ColPattern* | *metapropriedade*]...]  
  
 *ColName*  
 É o nome de coluna no conjunto de linhas.  
  
 *ColType*  
 É o tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da coluna no conjunto de linhas. Se os tipos de coluna diferem subjacente **xml** tipo de dados do atributo, coerção de tipo ocorre.  
  
 *ColPattern*  
 É um padrão geral  XPath opcional que descreve como os nós XML devem ser mapeados para as colunas. Se *ColPattern* não for especificado, o mapeamento padrão (**centrado em atributo** ou **centrado em elemento** mapeia conforme especificado por *sinalizadores* ) ocorra.  
  
 O padrão XPath especificado como *ColPattern* é usado para especificar a natureza especial do mapeamento (no caso de **centrado em atributo** e **centrado em elemento** mapeamento) que sobrescreve ou aprimora o mapeamento padrão indicado por *sinalizadores*.  
  
 O padrão geral XPath especificado como *ColPattern* também oferece suporte a metapropriedades.  
  
 *Metapropriedade*  
 É uma das metapropriedades fornecidas por OPENXML. Se *metapropriedade* for especificado, a coluna contém as informações fornecidas pela metapropriedade. As metapropriedades permitem extrair informações (como a posição relativa e informações de namespace) sobre nós XML. Isso fornece mais informações que as visíveis na representação textual.  
  
 *Nome de tabela*  
 É o nome da tabela que pode ser fornecido (em vez de *SchemaDeclaration*) se já existe uma tabela com o esquema desejado e nenhum padrão de coluna é necessário.  
  
## <a name="remarks"></a>Comentários  
 A cláusula WITH fornece um formato de conjunto de linhas (e as informações de mapeamento adicionais conforme necessário) usando o *SchemaDeclaration* ou especificando um existente *TableName*. Se a cláusula WITH opcional não for especificado, os resultados são retornados em uma **borda** formato de tabela. As tabelas de borda representam a estrutura de documento XML refinada (como nomes de elemento/atributo, a hierarquia de documento, os namespaces e PIS e assim por diante) em uma única tabela.  
  
 A tabela a seguir descreve a estrutura do **borda** tabela.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|É a ID exclusiva do nó do documento.<br /><br /> O elemento raiz tem um valor de ID 0. Os valores negativos da ID são reservados.|  
|**parentid**|**bigint**|Identifica o pai do nó. O pai identificado por essa ID não é necessariamente o elemento pai, mas depende do NodeType do nó cujo pai é identificado por essa ID. Por exemplo, se o nó for um nó de texto, o pai poderá ser um nó de atributo.<br /><br /> Se o nó estiver no nível superior no documento XML, seu **ParentID** será NULL.|  
|**NodeType**|**int**|Identifica o tipo de nó. É um inteiro que corresponde à numeração de tipo de nó XML DOM.<br /><br /> Os tipos de nó são:<br /><br /> 1 = Nó de elemento<br /><br /> 2 = Nó de atributo<br /><br /> 3 = Nó de texto|  
|**localname**|**nvarchar**|Fornece o nome local do elemento ou do atributo. Será NULL se o objeto DOM não tiver um nome.|  
|**prefixo**|**nvarchar**|É o prefixo do namespace do nome do nó.|  
|**namespaceuri**|**nvarchar**|É o URI do namespace do nó. Se o valor for NULL, nenhum namespace estará presente.|  
|**datatype**|**nvarchar**|É o tipo real de dados da linha de atributo ou de elemento, caso contrário será NULL. O tipo de dados é deduzido do DTD embutido ou do esquema embutido.|  
|**prev**|**bigint**|É a ID de XML do elemento irmão anterior. Será NULL se não houver nenhum irmão anterior direto.|  
|**text**|**ntext**|Contém o valor do atributo ou o conteúdo de elemento em forma de texto (ou será NULL se o **borda** entrada da tabela não requer um valor).|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. Usando uma instrução SELECT simples com OPENXML  
 O exemplo a seguir cria uma representação interna da imagem XML usando `sp_xml_preparedocument`. Uma instrução `SELECT` que usa um provedor de conjunto de linhas `OPENXML` é executada na representação interna do documento XML.  
  
 O *sinalizador* valor é definido como `1`. Isso indica **centrado em atributo** mapeamento. Portanto, os atributos XML mapeiam para as colunas no conjunto de linhas. O *rowpattern* especificado como `/ROOT/Customer` identifica o `<Customers>` nós a serem processados.  
  
 Opcional *ColPattern* parâmetro (padrão de coluna) não é especificado porque o nome da coluna corresponde aos nomes de atributo XML.  
  
 O provedor de conjunto de linhas `OPENXML` cria um conjunto de linhas de duas colunas (`CustomerID` e `ContactName`) das quais a instrução `SELECT` recupera as colunas necessárias (nesse caso, todas as colunas).  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Se o mesmo `SELECT` instrução for executada com *sinalizadores* definida como `2`, indicando que **centrado em elemento** mapeamento, os valores de `CustomerID` e `ContactName` para ambas as clientes no documento XML serão retornados como NULL, porque não há nenhum elemento chamado `CustomerID` ou `ContactName` no documento XML.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. Especificando ColPattern para mapeamento entre colunas e atributos XML  
 A consulta a seguir retorna ID de cliente, data do pedido, ID de produto e atributos de quantidade do documento XML. O *rowpattern* identifica o `<OrderDetails>` elementos. `ProductID` e `Quantity` são os atributos do elemento `<OrderDetails>`. Entretanto, `OrderID`, `CustomerID`e `OrderDate` são os atributos do elemento de pai (`<Orders>`).  
  
 Opcional *ColPattern* for especificado. Isso indica o seguinte:  
  
-   O `OrderID`, `CustomerID`, e `OrderDate` no mapa do conjunto de linhas para os atributos do pai de nós identificados por *rowpattern* no documento XML.  
  
-   O `ProdID` coluna no conjunto de linhas é mapeada para o `ProductID` atributo e o `Qty` coluna no conjunto de linhas é mapeada para o `Quantity` atributo de nós identificados em *rowpattern*.  
  
 Embora o **centrado em elemento** mapeamento for especificado o *sinalizadores* parâmetro, o mapeamento especificado em *ColPattern* substitui esse mapeamento.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. Obtendo resultados em um formato de tabela de borda  
 O documento XML de exemplo a seguir consiste nos elementos `<Customers>`, `<Orders>` e `<Order_0020_Details>`. Primeiro, **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o `OPENXML`.  
  
 No `OPENXML` instrução, o *rowpattern* (`/ROOT/Customers`) identifica o `<Customers>` nós para processar. Como a cláusula WITH não é fornecida, `OPENXML` retorna o conjunto de linhas em uma **borda** formato de tabela.  
  
 Por fim o `SELECT` instrução recupera todas as colunas a **borda** tabela.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos: usando OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
