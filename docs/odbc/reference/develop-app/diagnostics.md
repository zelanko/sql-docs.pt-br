---
title: Diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6ffbcdac7a478f8edd6560610811ddff6952b0d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="diagnostics"></a>diagnóstico
Funções em ODBC retornam informações de diagnóstico de duas maneiras. O código de retorno indica o êxito ou falha da função, geral, enquanto os registros de diagnóstico fornecem informações detalhadas sobre a função. Pelo menos um registro de diagnóstico, o registro de cabeçalho, será retornada mesmo se a função tiver êxito.  
  
 Informações de diagnóstico são usadas em tempo de desenvolvimento para capturar erros de programação como identificadores inválidos e erros de sintaxe em instruções de SQL embutido. Ele é usado em tempo de execução para capturar erros e avisos, como truncamento de dados, violações de acesso e erros de sintaxe em instruções SQL inseridas pelo usuário.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Exemplos de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
