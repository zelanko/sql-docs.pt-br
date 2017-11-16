---
title: "Remover índices XML | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01e16ed7ef2a64f4a04af9d683247d09c8942fe2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="drop-xml-indexes"></a>Descartar índices XML
  A instrução [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser usada para remover índices primários ou secundários XML e não XML existentes. No entanto nenhuma opção de DROP INDEX se aplica a índices XML. Se você descartar o índice XML primário, qualquer índice secundário que estiver presente também será excluído.  
  
 A sintaxe de DROP com *TableName.IndexName* está sendo desativada e não tem suporte para índices XML.  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>Exemplo: Criando e descartando um índice XML primário  
 No exemplo a seguir, um índice XML é criado em um tipo de coluna **xml** .  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 Quando uma tabela é descartada, todos os índices XML que ela contém também são descartados automaticamente. No entanto uma coluna XML não poderá ser descartada de uma tabela se existir um índice XML na coluna.  
  
 No exemplo a seguir, um índice XML é criado em um tipo de coluna **xml** . Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 Agora, é possível criar um índice de XML primário na `Co12`.  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>Exemplo: Criando um índice XML usando a opção de índice DROP_EXISTING  
 No exemplo a seguir, um índice XML é criado em uma coluna (`XmlColx`). Em seguida, outro índice XML com o mesmo nome é criado em uma coluna diferente (`XmlColy`). Como a opção `DROP_EXISTING` está especificada, o índice XML existente em (`XmlColx)` ) é descartado e um novo índice XML em (`XmlColy`) é criado.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 Essa consulta retorna o nome da coluna na qual o índice XML especificado é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
