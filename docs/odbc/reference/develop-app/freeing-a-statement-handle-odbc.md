---
title: Liberando um identificador de instrução ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305611"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar um identificador de instrução ODBC
Como mencionado anteriormente, é mais eficiente reutilizar instruções do que descartá-las e alocar novas. Antes de executar uma nova instrução SQL em uma instrução, os aplicativos devem ter certeza de que as configurações atuais da instrução são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, os parâmetros e os conjuntos de resultados para a instrução SQL antiga precisam ser desassociados (chamando **SQLFreeStmt** com as opções SQL_RESET_PARAMS e SQL_UNBIND) e reassociar para a nova instrução SQL.  
  
 Quando o aplicativo termina de usar a instrução, ele chama **SQLFreeHandle** para liberar a instrução. Depois de liberar a instrução, é um erro de programação de aplicativo usar o identificador da instrução em uma chamada para uma função ODBC; Isso tem conseqüências indefinidas, mas provavelmente fatais.  
  
 Quando **SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre a instrução.  
  
 **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.
