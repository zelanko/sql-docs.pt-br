---
title: Desconectando de uma fonte de dados ou driver | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300456"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectar de uma fonte de dados ou de um driver
Quando um aplicativo termina de usar uma fonte de dados, ele chama **SQLDisconnect**. O **SQLDisconnect** libera Todas as instruções que são alocadas na conexão e desconecta o driver da fonte de dados. Ele retornará um erro se uma transação estiver em andamento.  
  
 Após a desconexão, o aplicativo pode chamar **SQLFreeHandle** para liberar a conexão. Depois de liberar a conexão, é um erro de programação de aplicativo usar o identificador da conexão em uma chamada para uma função ODBC; Isso tem conseqüências indefinidas, mas provavelmente fatais. Quando **SQLFreeHandle** é chamado, o driver libera a estrutura usada para armazenar informações sobre a conexão.  
  
 O aplicativo também pode reutilizar a conexão, seja para se conectar a uma fonte de dados diferente ou reconectar-se à mesma fonte de dados. A decisão de permanecer conectada, em oposição à desconexão e reconexão posterior, requer que o gravador do aplicativo considere os custos relativos de cada opção; tanto a conexão com uma fonte de dados quanto a conexão restante podem ser relativamente dispendiosas dependendo da mídia de conexão. Ao fazer uma compensação correta, o aplicativo também deve fazer suposições sobre a probabilidade e o tempo de operações adicionais na mesma fonte de dados.
