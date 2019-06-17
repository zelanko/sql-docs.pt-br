---
title: Verificações de aviso e erro do Gerenciador de driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e00b6907d58cda1708cf61907d3c5ff6bf56edfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238032"
---
# <a name="driver-manager-error-and-warning-checks"></a>Verificações de aviso e de erro do Gerenciador de Driver
O Gerenciador de Driver totalmente ou parcialmente implementa várias funções e, portanto, verifica para todos ou alguns dos erros e avisos nessas funções.  
  
-   Implementa o Gerenciador de Driver **SQLDataSources** e **SQLDrivers** e verificações para todos os erros e avisos nessas funções.  
  
-   O Gerenciador de Driver que verifica se um driver implementa **SQLGetFunctions**. Se o driver não implementa **SQLGetFunctions**, o Gerenciador de Driver implementa e a verificação de todos os erros e avisos contidos nela.  
  
-   O Gerenciador de Driver implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, e **SQLGetDiagField** e verifica se há alguns erros nessas funções. Ele pode retornar os mesmos erros, pois o driver para algumas dessas funções porque ambos executam operações semelhantes. Por exemplo, o Gerenciador de Driver ou o driver pode retornar SQLSTATE IM008 (caixa de diálogo falhada) se um não consegue exibir uma caixa de diálogo de logon para **SQLDriverConnect**.
