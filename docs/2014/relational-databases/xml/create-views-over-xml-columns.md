---
title: Criar exibições sobre colunas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f575b1a21efa30d2317cff644b65c73150c4ac1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170177"
---
# <a name="create-views-over-xml-columns"></a>Criar exibições sobre colunas XML
  Você pode usar um `xml` coluna de tipo para criar modos de exibição. O exemplo a seguir cria um modo de exibição na qual o valor de uma `xml` coluna de tipo é recuperada usando o `value()` método da `xml` tipo de dados.  
  
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
  
 Observe os seguintes pontos sobre como usar o `xml` tipo de dados para criar exibições:  
  
-   O tipo de dados xml pode ser criado em uma exibição materializada. A exibição materializada não pode ser baseada em um método de tipo de dados xml. No entanto ela pode ser convertida em uma coleção de esquema XML diferente da coluna de tipo xml na tabela base.  
  
-   O `xml` tipo de dados não pode ser usado em exibições particionadas distribuídas.  
  
-   Predicados SQL que são executados em relação à exibição não serão enviados por push para o XQuery da definição da exibição.  
  
-   Métodos de tipo de dados XML em uma exibição não são atualizáveis.  
  
  
