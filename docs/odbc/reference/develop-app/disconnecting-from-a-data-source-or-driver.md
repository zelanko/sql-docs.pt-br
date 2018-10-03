---
title: Desconectar-se de dados de um fonte ou Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2189c0fcc65fd4192e94da140e2d55ac86826137
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706414"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectar de uma fonte de dados ou de um driver
Quando um aplicativo tiver terminado de usar uma fonte de dados, ele chama **SQLDisconnect**. **SQLDisconnect** libera todas as instruções que são alocadas a conexão e desconecta o driver da fonte de dados. Ele retornará um erro se uma transação está em processo.  
  
 Após a desconexão, o aplicativo pode chamar **SQLFreeHandle** para liberar a conexão. Depois de liberar a conexão, ele é um erro de programação de aplicativo para usar o identificador da conexão em uma chamada para uma função ODBC; Isso traz consequências indefinidas, mas provavelmente fatais. Quando **SQLFreeHandle** é chamado, as versões de driver a estrutura usada para armazenar informações sobre a conexão.  
  
 O aplicativo também pode reutilizar a conexão, para se conectar a uma fonte de dados diferente ou reconectar-se à mesma fonte de dados. A decisão de permanecer conectado, em vez de desconectar e reconectar posteriormente, requer que o criador do aplicativo considere os custos relativos de cada opção. tanto a se conectar a uma fonte de dados e permanecer conectado podem ser relativamente caros, dependendo da mídia de conexão. Ao fazer um equilíbrio correto, o aplicativo também deve fazer suposições sobre a probabilidade e o intervalo de outras operações na mesma fonte de dados.
