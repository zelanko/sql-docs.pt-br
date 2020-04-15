---
title: 'Passo 6: Desconecte-se da fonte de dados | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302787"
---
# <a name="step-6-disconnect-from-the-data-source"></a>Etapa 6: Desconectar-se da fonte de dados
O passo final é desconectar-se da fonte de dados, como mostrado na ilustração a seguir. Primeiro, o aplicativo libera qualquer alça de declaração ligando para **SQLFreeHandle**. Para obter mais informações, consulte [Freeing a Statement Handle .](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)  
  
 ![Mostra a desconexão de uma fonte de dados](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 Em seguida, o aplicativo se desconecta da fonte de dados com o **SQLDisconnect** e libera a alça de conexão com **o SQLFreeHandle**. Para obter mais informações, consulte [Desconectar-se de uma fonte de dados ou driver](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
 Finalmente, o aplicativo libera a alça do ambiente com **o SQLFreeHandle** e descarrega o Driver Manager. Para obter mais informações, consulte [Alocando a alça do ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).
