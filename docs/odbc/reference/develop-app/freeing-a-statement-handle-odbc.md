---
title: Liberando uma Declaração Lidar ODBC | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305611"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar um identificador de instrução ODBC
Como mencionado anteriormente, é mais eficiente reutilizar declarações do que solhá-las e alocar novas. Antes de executar uma nova declaração SQL em uma declaração, os aplicativos devem ter certeza de que as configurações atuais da declaração são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a antiga declaração SQL precisam ser desvinculados (ligando para **SQLFreeStmt** com as opções de SQL_RESET_PARAMS e SQL_UNBIND) e rebote para a nova declaração SQL.  
  
 Quando o aplicativo terminar de usar a declaração, ele chama **sqlfreehandle** para liberar a declaração. Depois de liberar a declaração, é um erro de programação de aplicativo usar a alça da declaração em uma chamada para uma função ODBC; fazê-lo tem consequências indefinidas, mas provavelmente fatais.  
  
 Quando **o SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre a declaração.  
  
 **O SQLDisconnect** libera automaticamente todas as instruções em uma conexão.
