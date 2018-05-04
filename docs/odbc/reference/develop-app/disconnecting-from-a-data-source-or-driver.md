---
title: Desconectar-se de dados de um fonte ou Driver | Microsoft Docs
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c99a2fb7c441c6de2a229895a1a68d68e9240c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectar-se de dados de um fonte ou Driver
Quando um aplicativo tiver terminado de usar uma fonte de dados, ele chama **SQLDisconnect**. **SQLDisconnect** libera todas as instruções que são alocadas a conexão e desconecta o driver da fonte de dados. Ele retorna um erro se uma transação está em processo.  
  
 Após a desconexão, o aplicativo pode chamar **SQLFreeHandle** para liberar a conexão. Depois de liberar a conexão, é um erro de programação de aplicativo para usar o identificador da conexão em uma chamada para uma função ODBC; Esse procedimento tem consequências indefinidas, mas provavelmente fatais. Quando **SQLFreeHandle** é chamado, as versões de driver a estrutura usada para armazenar informações sobre a conexão.  
  
 O aplicativo também pode reutilizar a conexão, para se conectar a uma fonte de dados diferente ou reconectar-se à mesma fonte de dados. A decisão de permanecer conectado, em vez de desconectar e reconectar posteriormente, requer que o gravador de aplicativos considerar os custos relativos de cada opção. tanto a conexão com uma fonte de dados e permanecer conectado podem ser relativamente caros, dependendo da mídia de conexão. Fazer um equilíbrio correto, o aplicativo também deve fazer suposições sobre a probabilidade e o intervalo de outras operações na mesma fonte de dados.
