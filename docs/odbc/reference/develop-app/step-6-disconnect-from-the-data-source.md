---
title: 'Etapa 6: desconectar da fonte de dados | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df8cd94435d74bf813b0b64be0753a0beb44d354
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302787"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Etapa 6: Desconectar-se da fonte de dados
A etapa final é desconectar da fonte de dados, conforme mostrado na ilustração a seguir. Primeiro, o aplicativo libera qualquer identificador de instrução chamando **SQLFreeHandle**. Para obter mais informações, consulte [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Mostra a desconexão de uma fonte de dados](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Em seguida, o aplicativo se desconecta da fonte de dados com **SQLDisconnect** e libera o identificador de conexão com **SQLFreeHandle**. Para obter mais informações, consulte [desconectando de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por fim, o aplicativo libera o identificador de ambiente com **SQLFreeHandle** e descarrega o Gerenciador de driver. Para obter mais informações, consulte [alocando o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
