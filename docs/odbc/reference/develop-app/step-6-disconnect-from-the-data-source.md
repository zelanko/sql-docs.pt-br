---
title: 'Etapa 6: Desconectar da fonte de dados | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65cc2ae8d2c2248a733e6efa9537fd3b40bb8fd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114117"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Etapa 6: Desconectar-se da fonte de dados
A etapa final é para se desconectar da fonte de dados, conforme mostrado na ilustração a seguir. Primeiro, o aplicativo libera quaisquer identificadores de instrução chamando **SQLFreeHandle**. Para obter mais informações, consulte [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Mostra a desconexão de uma fonte de dados](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Em seguida, o aplicativo desconecta da fonte de dados com **SQLDisconnect** e libera o identificador de conexão com **SQLFreeHandle**. Para obter mais informações, consulte [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por fim, o aplicativo libera o identificador de ambiente com **SQLFreeHandle** e descarrega o Gerenciador de Driver. Para obter mais informações, consulte [alocar o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
