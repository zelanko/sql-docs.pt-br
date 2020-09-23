---
description: excluir (XML DML)
title: excluir (XML DML)
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
- delete keyword
- delete statement [XML DML]
- deleting nodes
ms.assetid: b22c93a4-b84d-4356-af4c-6013322a4b71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6a553173716dae8a689c0731c568d43c6dec115
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116591"
---
# <a name="delete-xml-dml"></a>excluir (XML DML)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Exclui nós de uma instância XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
delete Expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *Expression*  
 É uma expressão XQuery que identifica os nós a serem excluídos. Todos os nós selecionados pela expressão, e também todos os nós ou valores que estão contidos nos nós selecionados, são excluídos. Conforme descrito em [insert (XML DML)](../../t-sql/xml/insert-xml-dml.md), essa referência deve ser a um nó existente no documento. Não pode ser um nó construído. A expressão não pode ser o nó de raiz (/). Se a expressão retornar uma sequência vazia, nenhuma exclusão ocorrerá e nenhum erro será retornado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-nodes-from-a-document-stored-in-an-untyped-xml-variable"></a>a. Excluindo nós de um documento armazenado em uma variável xml sem tipo  
 O exemplo a seguir ilustra como excluir vários nós de um documento. Primeiro, uma instância de XML é atribuída à variável do tipo **xml**. Depois, as instruções delete XML DML subsequentes excluem vários nós do documento.  
  
```sql
DECLARE @myDoc XML  
SET @myDoc = '<?Instructions for=TheWC.exe ?>   
<Root>  
 <!-- instructions for the 1st work center -->  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Some text 1  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
SELECT @myDoc  
  
-- delete an attribute  
SET @myDoc.modify('  
  delete /Root/Location/@MachineHours  
')  
SELECT @myDoc  
  
-- delete an element  
SET @myDoc.modify('  
  delete /Root/Location/step[2]  
')  
SELECT @myDoc  
  
-- delete text node (in <Location>  
SET @myDoc.modify('  
  delete /Root/Location/text()  
')  
SELECT @myDoc  
  
-- delete all processing instructions  
SET @myDoc.modify('  
  delete //processing-instruction()  
')  
SELECT @myDoc  
```  
  
### <a name="b-deleting-nodes-from-a-document-stored-in-an-untyped-xml-column"></a>B. Excluindo nós de um documento armazenado em uma coluna xml sem tipo  
 No exemplo a seguir, uma instrução **delete** XML DML remove o segundo elemento filho de <`Features`> do documento armazenado na coluna.  
  
```sql
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
GO
-- verify the contents before delete  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
-- delete the second feature  
UPDATE T  
SET x.modify('delete /Root/ProductDescription/Features/*[2]')  
-- verify the deletion  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O [Método modify() (tipo de dados xml)](../../t-sql/xml/modify-method-xml-data-type.md) é usado para especificar a palavra-chave **delete** de XML DML.  
  
-   O [Método query() (tipo de dados xml)](../../t-sql/xml/query-method-xml-data-type.md) é usado para consultar o documento.  
  
### <a name="c-deleting-nodes-from-a-typed-xml-column"></a>C. Excluindo nós de uma coluna xml com tipo  
 Este exemplo exclui nós de um documento XML de instruções de fabricação armazenado em uma coluna **xml** tipada.  
  
 No exemplo, primeiro você cria uma tabela (T) com uma coluna **xml** tipada no banco de dados AdventureWorks. Depois, você copia a instância XML de instruções de fabricação da coluna Instructions na tabela ProductModel para a tabela T e exclui um ou mais nós do documento.  
  
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
WHERE ProductModelID = 7  
GO  
SELECT Instructions  
FROM T  
--1) insert <Location 1000/>. Note: <Root> must be singleton in the query  
UPDATE T  
SET Instructions.modify('  
  DECLARE namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  INSERT <MI:Location LocationID="1000"  LaborHours="1000" >  
           These are manu steps at location 1000.   
           <MI:step>New step1 instructions</MI:step>  
           Instructions for step 2 are here  
           <MI:step>New step 2 instructions</MI:step>  
         </MI:Location>  
  AS first  
  INTO   (/MI:root)[1]  
')  
GO 
SELECT Instructions  
FROM T  
  
-- delete an attribute  
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/@LaborHours)   
')  
GO  
SELECT Instructions  
FROM T  
-- delete text in <location>  
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/text())   
')  
GO  
SET Instructions  
FROM T  
-- delete 2nd manu step at location 1000  
UPDATE T  
SET Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/MI:step[2])   
')  
GO  
SELECT Instructions  
FROM T  
-- cleanup  
DROP TABLE T  
GO 
```  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
