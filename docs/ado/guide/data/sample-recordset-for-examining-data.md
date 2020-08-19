---
description: Conjunto de registros de exemplo para examinar dados
title: Conjunto de registros de exemplo para examinar dados | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f4c989667d5b4a5ceb3fb0c4f4d929e49be92e00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452908"
---
# <a name="sample-recordset-for-examining-data"></a>Conjunto de registros de exemplo para examinar dados
Primeiro, vamos examinar o objeto **Recordset** como retornado usando a seguinte consulta SQL, executada em relação ao banco de dados de exemplo Northwind em Microsoft SQL Server.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 O objeto **Recordset** resultante contém todas as produzidas no banco de dados mostradas na tabela a seguir.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Pêras secas-orgânicas do tio Bob|30, 0|  
|14|Tofu|23,2500|  
|28|Rssle chucrute|45,6000|  
|51|Maçãs secas Manjimup|53, 0|  
|74|Longlife Tofu|10, 0|  
  
 Se você estiver interessado em obter esses resultados por conta própria, experimente o seguinte exemplo de JScript:  
  
-   [Exemplo de JScript para retornar um conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
