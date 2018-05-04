---
title: 'Etapa 6: Desconectar da fonte de dados | Microsoft Docs'
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
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9d35aa0d9f7fddb8aa713ca4ef9e6ec5f7968e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-6-disconnect-from-the-data-source"></a>Etapa 6: Desconectar da fonte de dados
A etapa final é desconectar da fonte de dados, conforme mostrado na ilustração a seguir. Primeiro, o aplicativo libera os identificadores de instrução chamando **SQLFreeHandle**. Para obter mais informações, consulte [liberando um identificador de instrução](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 ![Mostra a desconexão de uma fonte de dados](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Em seguida, o aplicativo se desconecta da fonte de dados com **SQLDisconnect** e libera o identificador de conexão com **SQLFreeHandle**. Para obter mais informações, consulte [desconectar-se de uma fonte de dados ou Driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Por fim, o aplicativo libera o identificador de ambiente com **SQLFreeHandle** e descarrega o Gerenciador de Driver. Para obter mais informações, consulte [ao alocar identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
