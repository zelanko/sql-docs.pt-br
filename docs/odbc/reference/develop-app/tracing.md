---
title: Rastreamento | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298043"
---
# <a name="tracing"></a>Rastreamento
O Gerenciador de driver ODBC tem um recurso de rastreamento que permite que a sequência de chamadas de função feita por um aplicativo ODBC seja gravada e transcrita em um arquivo de log. O rastreamento é executado por uma DLL de rastreamento que captura chamadas entre o aplicativo e o Gerenciador de driver e entre o Gerenciador de driver e o driver. Esse método de rastreamento substitui o rastreamento executado pelo Gerenciador de driver ODBC 2 *. x* e o rastreamento executado no ODBC 2 *. x* por meio do ODBC Spy.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [DLL de rastreamento](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Arquivo de rastreamento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Habilitar o rastreamento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md)
