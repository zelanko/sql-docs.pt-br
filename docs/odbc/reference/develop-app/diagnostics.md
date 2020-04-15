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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09f46d3fd6aa2f9b9c7310af6d3ddc90f78389f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305147"
---
# <a name="diagnostics"></a>Diagnósticos
Funções no retorno de informações de diagnóstico oDBC de duas maneiras. O código de retorno indica o sucesso geral ou a falha da função, enquanto os registros de diagnóstico fornecem informações detalhadas sobre a função. Pelo menos um registro de diagnóstico - o registro do cabeçalho - é devolvido mesmo que a função tenha sucesso.  
  
 As informações de diagnóstico são usadas na hora do desenvolvimento para capturar erros de programação, como alças inválidas e erros de sintaxe em instruções SQL codificadas. Ele é usado em tempo de execução para capturar erros e avisos de tempo de execução, como truncamento de dados, violações de acesso e erros de sintaxe em declarações SQL inseridas pelo usuário.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Registros de diagnóstico](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Usar SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementar SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Exemplos de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
