---
title: Nomes de mesa | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303117"
---
# <a name="table-names"></a>Nomes de tabela
Quando o driver dBASE, Microsoft Excel, Paradox ou Text é usado, os nomes de tabela que ocorrem na cláusula DE DE SELECT ou DELETE, após a cláusula INTO em INSERT, e após ATUALIZAÇÃO, TABELA DE CRIAÇÃO e TABELA DE GOTA podem conter um caminho válido, nome principal e extensão de nome do arquivo.  
  
 O uso de um nome de tabela em outro lugar em uma declaração SQL não suporta o uso de caminhos ou extensões, mas aceitará apenas o nome principal (por exemplo, EMP DE C:\ABC\EMP).  
  
 Nomes de correlação (pseudônimos) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
