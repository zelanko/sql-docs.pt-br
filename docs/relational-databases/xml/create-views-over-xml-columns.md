---
title: "Criar exibições sobre colunas XML | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00f455c27f3efdb2182e322112ce22f45abb4a51
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-views-over-xml-columns"></a>Criar exibições sobre colunas XML
  É possível usar uma coluna de tipo **xml** para criar exibições. O exemplo a seguir cria uma exibição na qual o valor de uma coluna de tipo `xml` é recuperada usando o método **value()** do tipo de dados **xml** .  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 Execute a consulta a seguir em relação à exibição:  
  
```  
SELECT *   
FROM   MyView  
```  
  
 Este é o resultado:  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 Observe os seguintes pontos sobre o uso do tipo de dados **xml** para criar exibições:  
  
-   O tipo de dados xml pode ser criado em uma exibição materializada. A exibição materializada não pode ser baseada em um método de tipo de dados xml. No entanto ela pode ser convertida em uma coleção de esquema XML diferente da coluna de tipo xml na tabela base.  
  
-   O tipo de dados **xml** não pode ser usado em Exibições Particionadas Distribuídas.  
  
-   Predicados SQL que são executados em relação à exibição não serão enviados por push para o XQuery da definição da exibição.  
  
-   Métodos de tipo de dados XML em uma exibição não são atualizáveis.  
  
  
