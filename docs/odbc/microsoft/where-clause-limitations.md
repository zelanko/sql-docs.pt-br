---
title: "ONDE cláusula limitações | Microsoft Docs"
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
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c55864642bced9895f8a6f5a408b8fbc1a216335
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="where-clause-limitations"></a>ONDE cláusula limitações
O número máximo de cláusulas em uma cláusula WHERE é 40.  
  
 Colunas LONGVARBINARY e LONGVARCHAR podem ser comparadas a literais de até 255 caracteres de comprimento, mas não podem ser comparadas usando parâmetros.
