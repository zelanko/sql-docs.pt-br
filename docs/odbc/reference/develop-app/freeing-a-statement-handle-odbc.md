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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc16e820671aa69c15365413d44fb9bcf807236b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757724"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar um identificador de instrução ODBC
Como mencionado anteriormente, é mais eficiente reutilizar as instruções que to soltá-los e alocar novos. Antes de executar uma nova instrução SQL em uma instrução, os aplicativos devem ser-se de que as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a instrução SQL antiga precisará ser desassociado (chamando **SQLFreeStmt** com as opções SQL_RESET_PARAMS e SQL_UNBIND) e a reassociação para a nova instrução SQL.  
  
 Quando o aplicativo tiver terminado de usar a instrução, ele chama **SQLFreeHandle** para liberar a instrução. Depois de liberar a instrução, ele é um erro de programação de aplicativo para usar o identificador da instrução em uma chamada para uma função ODBC; Isso traz consequências indefinidas, mas provavelmente fatais.  
  
 Quando **SQLFreeHandle** é chamado, as versões de driver a estrutura usada para armazenar informações sobre a instrução.  
  
 **SQLDisconnect** libera automaticamente todas as instruções em uma conexão.
