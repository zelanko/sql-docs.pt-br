---
title: Nomes de correlação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 535c169123923cdb36c355e098f6e0c55ebb9d56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127313"
---
# <a name="correlation-names"></a>Nomes de correlação
Nomes de correlação são totalmente compatíveis, incluindo dentro da lista de tabela. Por exemplo, na seguinte cadeia de caracteres, o E1 é o nome de correlação para a tabela chamada Emp:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
