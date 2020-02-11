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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a00861365df27357099176151bcd681e15e585e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985118"
---
# <a name="tracing"></a>Rastreamento
O Gerenciador de driver ODBC tem um recurso de rastreamento que permite que a sequência de chamadas de função feita por um aplicativo ODBC seja gravada e transcrita em um arquivo de log. O rastreamento é executado por uma DLL de rastreamento que captura chamadas entre o aplicativo e o Gerenciador de driver e entre o Gerenciador de driver e o driver. Esse método de rastreamento substitui o rastreamento executado pelo Gerenciador de driver ODBC 2 *. x* e o rastreamento executado no ODBC 2 *. x* por meio do ODBC Spy.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [DLL de rastreamento](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Arquivo de rastreamento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Habilitar o rastreamento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md)
