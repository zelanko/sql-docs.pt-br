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
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939784"
---
# <a name="table-names"></a>Nomes de tabela
Quando o dBASE, o Microsoft Excel, o Paradox ou o driver de texto são usados, os nomes de tabela que ocorrem na cláusula FROM de SELECT ou DELETE, após a cláusula INTO em INSERT, e após UPDATE, CREATE TABLE e DROP TABLE podem conter um caminho válido, um nome primário e uma extensão de nome de arquivo .  
  
 O uso de um nome de tabela em outro lugar em uma instrução SQL não oferece suporte ao uso de caminhos ou extensões, mas aceitará apenas o nome primário (por exemplo, EMP de C:\ABC\EMP).  
  
 Os nomes de correlação (aliases) podem ser usados. Por exemplo:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
