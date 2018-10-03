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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d72d7868d0e19719ea7992bdb8ccd1f61f3718d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755725"
---
# <a name="table-names"></a>Nomes de tabela
Quando o dBASE, Microsoft Excel, Paradox, ou texto driver é usado, nomes de tabela que ocorrem na cláusula FROM de SELECT ou DELETE, depois da cláusula INTO em INSERT e UPDATE, CREATE TABLE e DROP TABLE podem conter um caminho válido, nome primário e arquivo de extensão de nome .  
  
 Uso de um nome de tabela em outro lugar em uma instrução SQL não suporta o uso de caminhos ou extensões, mas aceitará somente o nome primário (por exemplo, EMP de C:\ABC\EMP).  
  
 Nomes de correlação (alias) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
