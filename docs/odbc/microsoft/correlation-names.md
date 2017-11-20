---
title: "Nomes de correlação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f757a0609490c280e2d6acb3679059e7f56dace
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="correlation-names"></a>Nomes de correlação
Nomes de correlação são totalmente suportados, incluindo, dentro da lista de tabela. Por exemplo, na cadeia de caracteres a seguir, E1 é o nome de correlação para a tabela chamada Emp:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```

