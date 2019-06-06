---
title: Para examinar dados de exemplo do conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9ffc34dd95ac2f5ef6e26e796c4c05cd91b28ae0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700392"
---
# <a name="sample-recordset-for-examining-data"></a>Conjunto de registros de exemplo para examinar dados
Primeiro, vamos examinar a **Recordset** objeto conforme retornados usando a seguinte consulta SQL, executada nos dados de exemplo Northwind base no Microsoft SQL Server.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 O resultante **Recordset** objeto contém todos os o produzirá no banco de dados mostrados na tabela a seguir.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Peras secas orgânico de tio Bob|30.0000|  
|14|Bananas|23.2500|  
|28|Rssle chucrute|45.6000|  
|51|Maçãs Secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 Se você estiver interessado em obter esses resultados por conta própria, experimente o seguinte exemplo de JScript:  
  
-   [Exemplo de JScript para retornar um conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
