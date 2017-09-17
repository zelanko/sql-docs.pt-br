---
title: "ONDE cláusula limitações | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3169ef45acb26b6db6bbb46680163575d5a588f4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="where-clause-limitations"></a>ONDE cláusula limitações
O número máximo de cláusulas em uma cláusula WHERE é 40.  
  
 Colunas LONGVARBINARY e LONGVARCHAR podem ser comparadas a literais de até 255 caracteres de comprimento, mas não podem ser comparadas usando parâmetros.
