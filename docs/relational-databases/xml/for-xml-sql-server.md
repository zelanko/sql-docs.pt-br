---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: 5d497064378b7fe34c95ffe9c886144bb3523256
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67943339"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Uma consulta SELECT retorna resultados como um conjunto de linhas. Opcionalmente, é possível recuperar resultados formais de uma consulta SQL como XML com a especificação da cláusula FOR XML na consulta. A cláusula FOR XML pode ser usada em consultas de nível superior e em subconsultas. A cláusula FOR XML de nível superior pode ser usada apenas na instrução SELECT. Em subconsultas, FOR XML pode ser usado nas instruções INSERT, UPDATE e DELETE. FOR XML também pode ser usado em instruções de atribuição.

Em uma cláusula FOR XML, você especifica um destes modos:

- RAW
- AUTO
- EXPLICIT
- PATH

O modo RAW gera um único elemento \<row> por linha no conjunto de linhas retornado pela instrução SELECT. É possível gerar hierarquia de XML escrevendo consultas FOR XML aninhadas.

O modo AUTO gera aninhamento no XML resultante usando heurística com base na maneira como a instrução SELECT é especificada. Você tem controle mínimo sobre a forma do XML gerado. As consultas FOR XML aninhadas podem ser escritas para gerar hierarquia de XML além da forma do XML gerada pela heurística do modo AUTO.

O modo EXPLICIT permite mais controle sobre a forma do XML. É possível misturar atributos e elementos à vontade para decidir a forma do XML. Um formato específico é necessário para o conjunto de linhas resultante que é gerado por causa da execução da consulta. Em seguida, esse formato do conjunto de linhas é mapeado na forma do XML. A força do modo EXPLICIT é misturar atributos e elementos à vontade, criar wrappers e propriedades aninhadas complexas, criar valores separados por espaços (por exemplo, o atributo OrderID pode ter uma lista de valores de ID de ordem) e conteúdo misto.

No entanto, a escrita de consultas no modo EXPLICIT pode ser trabalhosa. É possível usar algumas das novas funcionalidades de FOR XML, como escrita da diretiva TYPE e de consultas no modo FOR XML RAW/AUTO/PATH, em vez de usar o modo EXPLICIT para gerar as hierarquias. As consultas FOR XML aninhadas podem produzir qualquer XML que possa ser gerado usando o modo EXPLICIT. Para obter mais informações, consulte [Usar consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md) e [Diretiva TYPE em consultas FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).

O modo PATH em conjunto com a funcionalidade de consulta FOR XML aninhada fornece a flexibilidade do modo EXPLICIT de uma maneira mais simples.

Esses modos estão em efeito apenas para a execução da consulta para a qual eles estão definidos. Eles não afetam os resultados de nenhuma consulta subsequente.

FOR XML não é válido para nenhuma seleção usada com uma cláusula FOR BROWSE.

## <a name="example"></a>Exemplo

A instrução `SELECT` a seguir recupera informações das tabelas `Sales.Customer` e `Sales.SalesOrderHeader` o banco de dados `AdventureWorks2012` . Essa consulta especifica o modo `AUTO` na cláusula `FOR XML` :

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>Cláusula FOR XML e nomes de servidores

Quando uma instrução SELECT com uma cláusula FOR XML especifica um nome de quatro partes na consulta, o nome do servidor não é retornado no documento XML resultante quando a consulta é executada no computador local. No entanto o nome do servidor é retornado como o nome de quatro partes quando a consulta é executada em um servidor de rede.

Por exemplo, considere esta consulta:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**Servidor local:** &nbsp; Quando `ServerName` for um servidor local, a consulta retornará o seguinte texto:

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**Servidor de rede**: &nbsp; Quando `ServerName` for um servidor de rede, a consulta retornará o seguinte texto:

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**Evitar ambiguidade**: &nbsp; Essa ambiguidade potencial pode ser evitada especificando este alias:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

Agora, a consulta não ambígua retorna o seguinte texto:

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>Consulte Também

[Sintaxe básica da cláusula FOR XML](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[Usar o modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
