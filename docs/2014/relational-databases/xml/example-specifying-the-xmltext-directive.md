---
title: 'Exemplo: Especificando a diretiva XMLTEXT | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75f04b8dfb6cfec70c6fc141178dfb56c9ffd94c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205093"
---
# <a name="example-specifying-the-xmltext-directive"></a>Exemplo: Especificando a diretiva XMLTEXT
  Este exemplo ilustra como dados na coluna de estouro são resolvidos usando a diretiva `XMLTEXT` em uma instrução `SELECT` no modo EXPLICIT.  
  
 Considere a tabela `Person` . Esta tabela tem uma coluna `Overflow` que armazena a parte não consumida do documento XML.  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 Essa consulta recupera colunas da tabela `Person` . Para a coluna `Overflow` , *AttributeName* não é especificado, mas *directive* é definida como `XMLTEXT` , como parte do fornecimento de um nome de coluna da tabela universal.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEST] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 No documento XML resultante:  
  
-   Como *AttributeName* não está especificado para a coluna `Overflow` e a diretiva `xmltext` está especificada, os atributos no elemento <`overflow`> são acrescentados à lista de atributos do elemento <`Parent`> de fechamento.  
  
-   Como o atributo `PersonID` no elemento <`xmltext`> entra em conflito com o atributo `PersonID` recuperado no mesmo nível de elemento, o atributo no elemento <`xmltext`> é ignorado, mesmo que `PersonID` seja NULL. Geralmente, um atributo substitui um atributo do mesmo nome no estouro.  
  
 Esse é o resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>`  
  
 Se os dados de estouro tiverem subelementos e a mesma consulta for especificada, os subelementos na coluna `Overflow` serão adicionados como os subelementos do elemento <`Parent`> de circunscrição.  
  
 Por exemplo, altere os dados na tabela `Person` para que a coluna `Overflow` agora tenha subelementos.  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 Se a mesma consulta for executada, os subelementos no elemento <`xmltext`> serão adicionados como subelementos do elemento <`Parent`> de circunscrição:  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Esse é o resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `</Parent>`  
  
 Se *AttributeName* for especificado com a diretiva `xmltext`, os atributos do elemento <`overflow`> serão adicionados como atributos dos subelementos do elemento <`Parent`> de circunscrição. O nome especificado para *AttributeName* se torna o nome do subelemento.  
  
 Nesta consulta, *AttributeName*, <`overflow`> é especificado junto com a diretiva `xmltext`*:*  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 Esse é o resultado:  
  
 `<Parent PersonID="P1" PersonName="Joe">`  
  
 `<overflow attr1="data">content</overflow>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe">`  
  
 `<overflow attr2="data" />`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe">`  
  
 `<overflow attr3="data" PersonID="P">`  
  
 `<name>PersonName</name>`  
  
 `</overflow>`  
  
 `</Parent>`  
  
 Neste elemento de consulta, *directive* está especificada para o atributo `PersonName`. Isso resulta na adição de `PersonName` como um subelemento do elemento <`Parent`> de circunscrição. Os atributos do <`xmltext`> ainda estão anexados ao elemento <`Parent`> de circunscrição. O conteúdo do elemento e subelementos de <`overflow`> são pré-anexados a outros subelementos dos elementos <`Parent`> de circunscrição.  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Esse é o resultado:  
  
 `<Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" attr2="data">`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 Se os dados da coluna `XMLTEXT` contiverem atributos no elemento raiz, esses atributos não serão mostrados no esquema de dados XML e o analisador MSXML não validará o fragmento do documento XML resultante. Por exemplo:  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 Este é o resultado. Observe que no esquema retornado, o atributo de estouro `a` não será encontrado no esquema:  
  
 `<Schema name="Schema2"`  
  
 `xmlns="urn:schemas-microsoft-com:xml-data"`  
  
 `xmlns:dt="urn:schemas-microsoft-com:datatypes">`  
  
 `<ElementType name="overflow" content="mixed" model="open">`  
  
 `</ElementType>`  
  
 `</Schema>`  
  
 `<overflow xmlns="x-schema:#Schema2" a="1">`  
  
 `</overflow>`  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo EXPLICIT com FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
