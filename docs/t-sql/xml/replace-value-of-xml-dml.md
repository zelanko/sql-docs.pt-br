---
description: substituir o valor de (XML DML)
title: substituir o valor de (XML DML)
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- update keyword
- replacement values [XML DML]
- updating node values
- replace value of XML DML statement
ms.assetid: c310f6df-7adf-493b-b56b-8e3143b13ae7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7efecb0dbecf4ae7e4d9d142eb6f3bff3f94d616
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116539"
---
# <a name="replace-value-of-xml-dml"></a>substituir o valor de (XML DML)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Atualiza o valor de um nó no documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
replace value of Expression1   
with Expression2  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*Expression1*  
Identifica um nó cujo valor será atualizado. Deve identificar apenas um único nó. Ou seja, a *Expression1* precisa ser um singleton estático. Se o XML for digitado, o tipo do nó deverá ser um tipo simples. Quando forem selecionados vários nós, um erro será gerado. Se *Expression1* retornar uma sequência vazia, não ocorrerá nenhuma substituição de valor e nenhum erro será retornado. *Expression1* precisa retornar um único elemento que tenha um conteúdo de tipo simples (tipos de lista ou atômicos), um nó de texto ou um nó de atributo. *Expression1* não pode ser um tipo de união, um tipo complexo, uma instrução de processamento, um nó de documento nem um nó de comentário ou um erro será retornado.  
  
*Expression2*  
Identifica o novo valor do nó. Pode ser uma expressão que retorna um nó tipo simples, porque **data()** será usado implicitamente. Se o valor for uma lista de valores, a instrução **update** substituirá o valor antigo pela lista. Ao modificar uma instância XML tipada, *Expression2* precisará ser do mesmo tipo ou de um subtipo da *Expression*1. Caso contrário, um erro é retornado. Ao modificar uma instância XML não tipada, *Expression2* precisará ser uma expressão que possa ser atomizada. Caso contrário, um erro é retornado.  
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir da instrução XML DML **replace value of** ilustra como atualizar nós em um documento XML.  
  
### <a name="a-replacing-values-in-an-xml-instance"></a>a. Substituindo valores em uma instância XML  
No exemplo a seguir, uma instância de documento é atribuída primeiro a uma variável do tipo **XML**. Em seguida, as instruções XML DML **replace value of** atualizam os valores no documento.  
  
```sql
DECLARE @myDoc XML;  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Manufacturing steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>';  
SELECT @myDoc;  
  
-- update text in the first manufacturing step  
SET @myDoc.modify('  
  replace value of (/Root/Location/step[1]/text())[1]  
  with "new text describing the manu step"  
');  
SELECT @myDoc;  
-- update attribute value  
SET @myDoc.modify('  
  replace value of (/Root/Location/@LaborHours)[1]  
  with "100.0"  
');  
SELECT @myDoc;  
```  
  
O destino atualizado deve ser, no máximo, um nó que seja explicitamente especificado na expressão de caminho adicionando um "[1]" no fim da expressão.  
  
### <a name="b-using-the-if-expression-to-determine-replacement-value"></a>B. Usando a expressão if para determinar o valor de substituição  
É possível especificar a expressão **if** na Expression2 da instrução **replace value of XML DML**, como mostra o exemplo a seguir. Expression1 identifica que o atributo LaborHours do primeiro centro de trabalho será atualizado. A Expression2 usa uma expressão **if** para determinar o novo valor do atributo LaborHours.  
  
```sql
DECLARE @myDoc XML  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours=".1"  
            MachineHours=".2" >Manu steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
--SELECT @myDoc  
  
SET @myDoc.modify('  
  replace value of (/Root/Location[1]/@LaborHours)[1]  
  with (  
       if (count(/Root/Location[1]/step) > 3) then  
         "3.0"  
       else  
          "1.0"  
      )  
')  
SELECT @myDoc  
```  
  
### <a name="c-updating-xml-stored-in-an-untyped-xml-column"></a>C. Atualizando XML armazenado em uma coluna XML sem tipo  
O exemplo a seguir atualiza XML armazenado em uma coluna:  
  
```sql
DROP TABLE T  
GO  
CREATE TABLE T (i INT, x XML)  
GO  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the current <ProductDescription> element  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
-- update the ProductName attribute value  
UPDATE T  
SET x.modify('  
  replace value of (/Root/ProductDescription/@ProductName)[1]  
  with "New Road Bike" ')  
-- verify the update  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
```  
  
### <a name="d-updating-xml-stored-in-a-typed-xml-column"></a>D. Atualizando XML armazenado em uma coluna XML com tipo  
Este exemplo substitui os valores em um documento de instruções de fabricação armazenado em uma coluna XML digitada.  
  
No exemplo, primeiro você cria uma tabela (T) com uma coluna XML digitada no banco de dados AdventureWorks. Depois, você copia a instância XML de instruções de fabricação da coluna Instructions na tabela ProductModel para a tabela T. Em seguida, as inserções são aplicadas ao XML na tabela T.  
  
```sql
USE AdventureWorks  
GO  
DROP TABLE T  
GO  
CREATE TABLE T(
  ProductModelID INT PRIMARY KEY,   
  Instructions XML (Production.ManuInstructionsSchemaCollection))  
GO  
INSERT T   
SELECT ProductModelID, Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=7  
GO
--insert a new location - <Location 1000/>.   
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
insert <MI:Location LocationID="1000"  LaborHours="1000"  LotSize="1000" >  
           <MI:step>Do something using <MI:tool>hammer</MI:tool></MI:step>  
         </MI:Location>  
  as first  
  into (/MI:root)[1]  
')  
GO  
SELECT Instructions  
FROM T  
GO  
-- Now replace manu. tool in location 1000  
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/MI:step/MI:tool)[1]   
  with "screwdriver"  
')  
GO  
SELECT Instructions  
FROM T  
-- Now replace value of lot size  
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/@LotSize)[1]   
  with 500 cast as xs:decimal ?  
')  
GO  
SELECT Instructions  
FROM T  
```  
  
Observe o uso de **cast** ao substituir o valor de LotSize. Isso é necessário quando o valor deve ser de um tipo específico. Neste exemplo, se 500 fosse o valor, a conversão explícita não seria necessária.  
  
## <a name="see-also"></a>Consulte Também  
[Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
[Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
[Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
[XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
