---
title: Seqüência de Registros de Status | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304167"
---
# <a name="sequence-of-status-records"></a>Sequência de registros de status
Se dois ou mais registros de status forem devolvidos, o Driver Manager e o driver os classificarão de acordo com as seguintes regras. O recorde com o posto mais alto é o primeiro recorde. A fonte de um registro (Driver Manager, driver, gateway, e assim por diante) não é considerada quando os registros de classificação.  
  
-   **Erros** Registros de status que descrevem erros têm a classificação mais alta. Entre os registros de erro, registros que indicam uma falha de transação ou possível falha de transação superam todos os outros registros. Se dois ou mais registros descreverem a mesma condição de erro, os SQLSTATEs definidos pela especificação CLI do Grupo Aberto (classes 03 a HZ) superam os SQLSTATEs definidos pelo ODBC e definidos pelo driver.  
  
-   **Sem valores de dados definidos pela implementação** Os registros de status que descrevem os valores sem dados definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** Os registros de status que descrevem avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descreverem a mesma condição de aviso, os SQLSTATEs de aviso definidos pela especificação CLI do Grupo Aberto superam os SQLSTATEs definidos pelo ODBC e definidos pelo driver.  
  
 Se há dois ou mais registros com a classificação mais alta, é indefinido qual registro é o primeiro registro. A ordem de todos os outros registros é indefinida. Em particular, como os avisos podem aparecer antes de erros, os aplicativos devem verificar todos os registros de status quando uma função retorna um valor diferente SQL_SUCCESS.
