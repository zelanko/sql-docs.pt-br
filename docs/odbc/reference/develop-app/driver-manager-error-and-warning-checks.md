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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce87b9dbed8cfa6ca621cb72c36220c13ecb0929
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e erro do Gerenciador de driver
O Gerenciador de Driver completamente ou parcialmente implementa um número de funções e, portanto, verifica todos ou alguns dos erros e avisos nessas funções.  
  
-   O Gerenciador de Driver implementa **SQLDataSources** e **SQLDrivers** e procura todos os erros e avisos nessas funções.  
  
-   O Gerenciador de Driver verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementa **SQLGetFunctions**, o Gerenciador de Driver implementa e a verificação de todos os erros e avisos nele.  
  
-   O Gerenciador de Driver implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, e **SQLGetDiagField** e verifica se há alguns erros nessas funções. Pode retornar os mesmos erros como o driver para algumas dessas funções porque ambos executam operações semelhantes. Por exemplo, o Gerenciador de Driver ou o driver pode retornar SQLSTATE IM008 (caixa de diálogo falhada) se qualquer um é não é possível exibir uma caixa de diálogo de logon para **SQLDriverConnect**.

