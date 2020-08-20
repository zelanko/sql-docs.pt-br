---
description: Nomes de tabela
title: Nomes de tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b264999f800e4387099240526f558110c39e27a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471454"
---
# <a name="table-names"></a>Nomes de tabela
Quando o dBASE, o Microsoft Excel, o Paradox ou o driver de texto são usados, os nomes de tabela que ocorrem na cláusula FROM de SELECT ou DELETE, após a cláusula INTO em INSERT, e após UPDATE, CREATE TABLE e DROP TABLE podem conter um caminho, um nome primário e uma extensão de nome de arquivo válidos.  
  
 O uso de um nome de tabela em outro lugar em uma instrução SQL não oferece suporte ao uso de caminhos ou extensões, mas aceitará apenas o nome primário (por exemplo, EMP de C:\ABC\EMP).  
  
 Os nomes de correlação (aliases) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
