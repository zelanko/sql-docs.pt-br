---
title: "Verificações de aviso e erro do Gerenciador de driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06da9cd5cee6b22d04689b50fb90a7a594f4685e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e erro do Gerenciador de driver
O Gerenciador de Driver completamente ou parcialmente implementa um número de funções e, portanto, verifica todos ou alguns dos erros e avisos nessas funções.  
  
-   O Gerenciador de Driver implementa **SQLDataSources** e **SQLDrivers** e procura todos os erros e avisos nessas funções.  
  
-   O Gerenciador de Driver verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementa **SQLGetFunctions**, o Gerenciador de Driver implementa e a verificação de todos os erros e avisos nele.  
  
-   O Gerenciador de Driver implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, e **SQLGetDiagField** e verifica se há alguns erros nessas funções. Pode retornar os mesmos erros como o driver para algumas dessas funções porque ambos executam operações semelhantes. Por exemplo, o Gerenciador de Driver ou o driver pode retornar SQLSTATE IM008 (caixa de diálogo falhada) se qualquer um é não é possível exibir uma caixa de diálogo de logon para **SQLDriverConnect**.
