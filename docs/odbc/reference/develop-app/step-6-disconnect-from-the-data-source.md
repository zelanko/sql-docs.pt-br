---
title: 'Etapa 6: Desconectar da fonte de dados | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 078471ba5f6f95d20a03d6e5191de0df2d8bdd9c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="step-6-disconnect-from-the-data-source"></a>Etapa 6: Desconectar da fonte de dados
A etapa final é desconectar da fonte de dados, conforme mostrado na ilustração a seguir. Primeiro, o aplicativo libera os identificadores de instrução chamando **SQLFreeHandle**. Para obter mais informações, consulte [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Mostra a desconexão de uma fonte de dados](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Em seguida, o aplicativo se desconecta da fonte de dados com **SQLDisconnect** e libera o identificador de conexão com **SQLFreeHandle**. Para obter mais informações, consulte [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por fim, o aplicativo libera o identificador de ambiente com **SQLFreeHandle** e descarrega o Gerenciador de Driver. Para obter mais informações, consulte [ao alocar identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
