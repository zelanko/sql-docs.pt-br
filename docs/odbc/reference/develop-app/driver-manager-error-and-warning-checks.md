---
title: Verificação de erro e aviso do driver manager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305777"
---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e de erro do Gerenciador de Driver
O Driver Manager implementa total ou parcialmente uma série de funções e, portanto, verifica todos ou alguns dos erros e avisos nessas funções.  
  
-   O Driver Manager implementa **SQLDataSources** e **SQLDrivers** e verifica todos os erros e avisos nessas funções.  
  
-   O Gerenciador de driver verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementar **SQLGetFunctions,** o Driver Manager implementará e verificará todos os erros e avisos nele.  
  
-   O Driver Manager implementa parcialmente **SQLAllocHandle,** **SQLConnect,** **SQLDriverConnect,** **SQLBrowseConnect,** **SQLFreeHandle,** **SQLGetDiagRec**e **SQLGetDiagField** e verifica se há alguns erros nessas funções. Ele pode retornar os mesmos erros que o driver para algumas dessas funções, porque ambos executam operações semelhantes. Por exemplo, o Gerenciador de driver ou o driver podem retornar sqlstate IM008 (falha de diálogo) se qualquer um não puder exibir uma caixa de diálogo de login para **SQLDriverConnect**.
