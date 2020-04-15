---
title: Desconectando-se de uma fonte de dados ou driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300456"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectar de uma fonte de dados ou de um driver
Quando um aplicativo é concluído usando uma fonte de dados, ele chama **SQLDisconnect**. **O SQLDisconnect** libera quaisquer instruções que estejam alocadas na conexão e desconecta o driver da fonte de dados. Ele retorna um erro se uma transação estiver em processo.  
  
 Após a desconexão, o aplicativo pode chamar **sqlfreehandle** para liberar a conexão. Depois de liberar a conexão, é um erro de programação de aplicativo usar a alça da conexão em uma chamada para uma função ODBC; fazê-lo tem consequências indefinidas, mas provavelmente fatais. Quando **o SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre a conexão.  
  
 O aplicativo também pode reutilizar a conexão, seja para se conectar a uma fonte de dados diferente ou se reconectar à mesma fonte de dados. A decisão de permanecer conectado, em vez de desconectar e reconectar posteriormente, exige que o autor do aplicativo considere os custos relativos de cada opção; tanto a conexão a uma fonte de dados quanto a permanência conectada podem ser relativamente caras dependendo do meio de conexão. Ao fazer uma troca correta, o aplicativo também deve fazer suposições sobre a probabilidade e o tempo de novas operações na mesma fonte de dados.
