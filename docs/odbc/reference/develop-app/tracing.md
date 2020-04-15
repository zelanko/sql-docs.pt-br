---
title: Traçando | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a08047409b203916fe5403cf28802d8570647cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298043"
---
# <a name="tracing"></a>Rastreamento
O Gerenciador de Driver oDBC tem uma facilidade de rastreamento que permite que a seqüência de chamadas de função feitas por um aplicativo ODBC seja gravada e transcrita em um arquivo de log. O rastreamento é realizado por um dll de rastreamento que captura chamadas entre o aplicativo e o Driver Manager, e entre o Driver Manager e o driver. Este método de rastreamento substitui o rastreamento realizado pelo ODBC*2.x* Driver Manager e o rastreamento realizado no ODBC 2 *.x* pelo ODBC Spy.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [DLL de rastreamento](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Arquivo de rastreamento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Habilitar o rastreamento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md)
