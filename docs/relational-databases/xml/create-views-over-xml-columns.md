---
title: Criar exibições sobre colunas XML | Microsoft Docs
description: Saiba como criar uma exibição na qual o valor de uma coluna de tipo xml é recuperada usando o método value() do tipo de dados xml.
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d4a9d8d0aa40f8454a2bd0fd089022630c34ca2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85691533"
---
# <a name="create-views-over-xml-columns"></a>Criar exibições sobre colunas XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
  
