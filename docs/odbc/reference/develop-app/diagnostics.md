---
title: Diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e79d377371277720e2fcc15a31ce715693d832
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63242293"
---
# <a name="diagnostics"></a>Diagnóstico
Funções no ODBC retornam informações de diagnóstico de duas maneiras. O código de retorno indica o êxito ou falha da função, geral, enquanto os registros de diagnóstico fornecem informações detalhadas sobre a função. Pelo menos um registro de diagnóstico - registro de cabeçalho - será retornado, mesmo se a função for bem-sucedida.  
  
 Informações de diagnóstico são usadas no momento do desenvolvimento para capturar erros de programação, como identificadores inválidos e erros de sintaxe em instruções de SQL embutido em código. Ele é usado em tempo de execução para capturar erros de tempo de execução e avisos, como truncamento de dados, violações de acesso e erros de sintaxe em instruções SQL inseridas pelo usuário.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Exemplos de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
