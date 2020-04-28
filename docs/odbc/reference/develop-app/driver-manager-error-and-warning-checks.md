---
title: Verificações de erro e aviso do Gerenciador de driver | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305777"
---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e de erro do Gerenciador de Driver
O Gerenciador de Driver implementa de forma completa ou parcial várias funções e, portanto, verifica todos os erros e avisos nessas funções.  
  
-   O Gerenciador de Driver implementa **SQLDataSources** e **sqldriveers** e verifica todos os erros e avisos nessas funções.  
  
-   O Gerenciador de driver verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementar **SQLGetFunctions**, o Gerenciador de Driver implementa e verifica todos os erros e avisos nele.  
  
-   O Gerenciador de Driver implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**e **SQLGetDiagField** e verifica alguns erros nessas funções. Ele pode retornar os mesmos erros que o driver para algumas dessas funções porque ambos executam operações semelhantes. Por exemplo, o driver ou o Gerenciador de driver pode retornar SQLSTATE IM008 (falha na caixa de diálogo) se qualquer um não puder exibir uma caixas de diálogo de logon para **SQLDriverConnect**.
