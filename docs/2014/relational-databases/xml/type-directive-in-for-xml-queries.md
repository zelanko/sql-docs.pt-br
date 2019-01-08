---
title: Diretiva TYPE em consultas FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bafe35efbcc1f5dae7cea0775464deac3c8ed7f8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351083"
---
# <a name="type-directive-in-for-xml-queries"></a>Diretiva TYPE em consultas FOR XML
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporte para o [xml &#40;Transact-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql) lhe permite solicitar opcionalmente que o resultado de uma consulta FOR XML seja retornado como `xml` tipo de dados, especificando a diretiva TYPE. Isso permite processar o resultado de uma consulta FOR XML no servidor. Por exemplo, você pode especificar uma consulta XQuery em relação a ela, atribuir o resultado a um `xml` variável de tipo, ou escrever [consultas FOR XML aninhadas](use-nested-for-xml-queries.md).  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna dados da instância de tipo de dados XML ao cliente como um resultado das diferentes construções pelo servidor como consultas FOR XML que usam a diretiva TYPE ou onde o tipo de dados `xml` é usado para retornar valores de dados da instância XML das colunas da tabela e dos parâmetros de saída SQL. No código do aplicativo cliente, o provedor ADO.NET solicita que essas informações de tipo de dados sejam enviadas em uma codificação binária do servidor. Porém, se você estiver usando FOR XML sem a diretiva TYPE, os dados XML retornarão como um tipo de cadeia de caracteres. De qualquer forma, o provedor cliente sempre poderá controlar qualquer formulário de XML. Observe que FOR XML de nível superior sem a diretiva TYPE não pode ser usado com cursores.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram o uso da diretiva TYPE com consultas FOR XML.  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>Recuperando resultados de consultas FOR XML como tipo xml  
 A consulta a seguir recupera informações de contato de clientes da tabela `Contacts` . Como a diretiva `TYPE` é especificada em `FOR XML`, o resultado é retornado como o tipo `xml`.  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 Este é o resultado parcial:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>Atribuindo resultados de consultas FOR XML a uma variável de tipo xml  
 No exemplo a seguir, um resultado de FOR XML é atribuído a uma variável de tipo `xml`, `@x`. A consulta recupera informações de contato, como o `BusinessEntityID`, `FirstName`, `LastName`, adicionais e números de telefone do `AdditionalContactInfo` coluna de `xml``TYPE`. Como a cláusula `FOR XML` especifica a diretiva `TYPE`, o XML é retornado como o tipo `xml` e é atribuído a uma variável.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>Consultando resultados de uma consulta FOR XML  
 As consultas FOR XML retornam XML. Portanto é possível aplicar métodos de tipo `xml`, como `query()` e `value()`, ao resultado XML retornado por consultas FOR XML.  
  
 Na consulta a seguir, o método `query()` do tipo de dados `xml` é usado para consultar o resultado da consulta `FOR XML`. Para obter mais informações, veja [Método query&#40;&#41; &#40;tipo de dados xml&#41;](/sql/t-sql/xml/query-method-xml-data-type).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 A consulta interna `SELECT ... FOR XML` retorna um resultado de tipo `xml` para o qual `SELECT` externo aplica o método `query()` ao tipo `xml`. Observe a diretiva `TYPE` especificada.  
  
 Esse é o resultado:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 Na consulta a seguir, o método `value()` do tipo de dados `xml` é usado para recuperar um valor do resultado XML retornado pela consulta `SELECT...FOR XML`. Para obter mais informações, veja [Método value&#40;&#41; &#40;tipo de dados XML&#41;](/sql/t-sql/xml/value-method-xml-data-type).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 A expressão de caminho XQuery no método `value()` recupera o primeiro número de telefone de contato de um cliente cujo `BusinessEntityID` é `1`.  
  
> [!NOTE]  
>  Se a diretiva TYPE não estiver especificada, o resultado da consulta FOR XML será retornado como tipo `nvarchar(max)`.  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>Usando resultados de consulta FOR XML em INSERT, UPDATE e DELETE (DML do Transact-SQL)  
 O exemplo a seguir demonstra como consultas FOR XML podem ser usadas em instruções DML (linguagem de manipulação de dados). No exemplo, o `FOR XML` retorna uma instância de tipo `xml`. A instrução `INSERT` insere esse XML em uma tabela.  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
