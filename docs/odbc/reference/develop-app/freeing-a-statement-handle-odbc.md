---
title: "Liberando um identificador de instrução ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b33d262c846d9ef8a41bf9440802664ac7d4b75f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-a-statement-handle-odbc"></a>Liberando um identificador de instrução ODBC
Como mencionado anteriormente, é mais eficiente reutilizar instruções que to descartá-los e alocar novos. Antes de executar uma nova instrução SQL em uma instrução, os aplicativos devem estar-se de que as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a instrução SQL antiga devem ser desassociado (chamando **SQLFreeStmt** com as opções SQL_RESET_PARAMS e SQL_UNBIND) e religação para a nova instrução SQL.  
  
 Quando o aplicativo terminar de usar a instrução, ele chama **SQLFreeHandle** para liberar a instrução. Depois de liberar a instrução, é um erro de programação de aplicativo para usar o identificador da instrução em uma chamada para uma função ODBC; Esse procedimento tem consequências indefinidas, mas provavelmente fatais.  
  
 Quando **SQLFreeHandle** é chamado, as versões de driver a estrutura usada para armazenar informações sobre a instrução.  
  
 **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.

