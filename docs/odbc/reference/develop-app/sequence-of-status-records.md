---
title: Sequência de registros de Status | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465912"
---
# <a name="sequence-of-status-records"></a>Sequência de registros de status
Se dois ou mais registros de status for retornados, o Gerenciador de Driver e o driver classificarão-las de acordo com as regras a seguir. O registro com a classificação mais alta é o primeiro registro. A origem de um registro (Gerenciador de Driver, driver, gateway e assim por diante) não é considerada quando registros de classificação.  
  
-   **Erros** registros de Status que descrevem os erros têm a classificação mais alta. Entre os registros de erro, os registros que indicam uma falha de transação ou a falha na transação possíveis outrank todos os outros registros. Se dois ou mais registros descrevem a mesma condição de erro, SQLSTATEs definidos pela especificação de CLI de grupo aberto (classes 03 por meio de HZ) outrank SQLSTATEs definidas pelo ODBC e definidos pelo driver.  
  
-   **Os valores de dados não definido pela implementação** registros de Status que descrevem os valores de dados não definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** registros de Status que descreve os avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descrevem a mesma condição de aviso, aviso SQLSTATEs definidos pela especificação de CLI de grupo aberto outrank SQLSTATEs definidas pelo ODBC e definidos pelo driver.  
  
 Se houver dois ou mais registros com a classificação mais alta, não está definido qual registro é o primeiro registro. A ordem de todos os outros registros é indefinida. Em particular, como avisos podem aparecer antes de erros, aplicativos devem verificar todos os registros de status, quando uma função retorna um valor diferente de SQL_SUCCESS.
