---
title: Nomes de tabela | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69af01ea73bfe8ad4f69cb9cae72e8579979ba61
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="table-names"></a>Nomes de tabela
Quando o dBASE, Microsoft Excel, Paradox, ou texto driver é usado, nomes de tabela que ocorrem na cláusula FROM de SELECT ou DELETE, depois da cláusula INTO em INSERT e UPDATE, CREATE TABLE e DROP TABLE podem conter um caminho válido, nome principal e arquivo de extensão de nome .  
  
 Uso de um nome de tabela em qualquer lugar em uma instrução SQL não suporta o uso de caminhos ou extensões mas aceitará somente o nome primário (por exemplo, EMP de C:\ABC\EMP).  
  
 Nomes de correlação (alias) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
