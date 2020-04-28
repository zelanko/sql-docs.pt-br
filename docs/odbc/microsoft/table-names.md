---
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
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303117"
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
