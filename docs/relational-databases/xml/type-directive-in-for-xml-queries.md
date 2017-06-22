---
title: Diretiva TYPE em consultas FOR XML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1e060f93c4aa26d86fbd6683099a66821c38e9b2
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="type-directive-in-for-xml-queries"></a>Diretiva TYPE em consultas FOR XML
  O suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md) permite solicitar opcionalmente que o resultado de uma consulta XML FOR seja retornado como o tipo de dados **xml**, especificando a diretiva TYPE. Isso permite processar o resultado de uma consulta FOR XML no servidor. Por exemplo, é possível especificar um XQuery nela, atribuir o resultado a uma variável de tipo **xml** ou gravar [Consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna dados da instância de tipo de dados XML ao cliente como resultado das diferentes construções pelo servidor como consultas FOR XML que usam a diretiva TYPE ou nos casos em que o tipo de dados **xml** é usado para retornar valores de dados da instância XML das colunas da tabela e dos parâmetros de saída SQL. No código do aplicativo cliente, o provedor ADO.NET solicita que essas informações de tipo de dados sejam enviadas em uma codificação binária do servidor. Porém, se você estiver usando FOR XML sem a diretiva TYPE, os dados XML retornarão como um tipo de cadeia de caracteres. De qualquer forma, o provedor cliente sempre poderá controlar qualquer formulário de XML. Observe que FOR XML de nível superior sem a diretiva TYPE não pode ser usado com cursores.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram o uso da diretiva TYPE com consultas FOR XML.  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>Recuperando resultados de consultas FOR XML como tipo xml  
 A consulta a seguir recupera informações de contato de clientes da tabela `Contacts` . Como a diretiva `TYPE` é especificada em `FOR XML`, o resultado é retornado como o tipo **xml** .  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 Este é o resultado parcial:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>Atribuindo resultados de consultas FOR XML a uma variável de tipo xml  
 No exemplo a seguir, um resultado de FOR XML é atribuído a uma variável de tipo **xml** , `@x`. A consulta recupera informações de contato, como `BusinessEntityID`, `FirstName`, `LastName`e números de telefone adicionais, na coluna `AdditionalContactInfo` de **xml**`TYPE`. Como a cláusula `FOR XML` especifica a diretiva `TYPE` , o XML é retornado como o tipo **xml** e é atribuído a uma variável.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>Consultando resultados de uma consulta FOR XML  
 As consultas FOR XML retornam XML. Portanto, é possível aplicar métodos de tipo **xml** , como **query()** e **value()**, ao resultado XML retornado por consultas FOR XML.  
  
 Na consulta a seguir, o método `query()` do tipo de dados **xml** é usado para consultar o resultado da consulta `FOR XML`. Para obter mais informações, veja [Método query&#40;&#41; &#40;tipo de dados xml&#41;](../../t-sql/xml/query-method-xml-data-type.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 A consulta interna `SELECT … FOR XML` retorna um resultado de tipo **xml** para o qual `SELECT` externo aplica o método `query()` ao tipo **xml**. Observe a diretiva `TYPE` especificada.  
  
 Este é o resultado:  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 Na consulta a seguir, o método `value()` do tipo de dados **xml** é usado para recuperar um valor do resultado XML retornado pela consulta `SELECT…FOR XML`. Para obter mais informações, veja [Método value&#40;&#41; &#40;tipo de dados XML&#41;](../../t-sql/xml/value-method-xml-data-type.md).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 A expressão de caminho XQuery no método `value()` recupera o primeiro número de telefone de contato de um cliente cujo `BusinessEntityID` é `1`.  
  
> [!NOTE]  
>  Se a diretiva TYPE não for especificada, o resultado da consulta FOR XML será retornado como o tipo **nvarchar(max)**.  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>Usando resultados de consulta FOR XML em INSERT, UPDATE e DELETE (DML do Transact-SQL)  
 O exemplo a seguir demonstra como consultas FOR XML podem ser usadas em instruções DML (linguagem de manipulação de dados). No exemplo, o `FOR XML` retorna uma instância do tipo **xml** . A instrução `INSERT` insere esse XML em uma tabela.  
  
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
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
