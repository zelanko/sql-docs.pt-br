---
title: Definição do nível de isolamento da transação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b575f9e208b5a1b7fa03b170b74633da149c67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750614"
---
# <a name="setting-the-transaction-isolation-level"></a>Configurar o nível de isolamento da transação
Para definir o nível de isolamento da transação, um aplicativo usa o atributo de conexão SQL_ATTR_TXN_ISOLATION. Se a fonte de dados não oferece suporte para o nível de isolamento solicitada, o driver ou fonte de dados pode definir um nível mais alto. Para determinar os níveis de isolamento da transação que uma fonte de dados oferece suporte e é o nível de isolamento padrão, um aplicativo chama **SQLGetInfo** com as opções SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Níveis mais altos de isolamento da transação oferecem a melhor proteção para a integridade do banco de dados. Transações serializáveis são a garantia de ser afetado por outras transações e, portanto, são garantidas para manter a integridade do banco de dados.  
  
 No entanto, um nível mais alto de isolamento da transação pode causar um desempenho mais lento porque aumenta as chances de que o aplicativo terá que aguardar os bloqueios em dados a serem liberados. Um aplicativo pode especificar um nível inferior de isolamento para aumentar o desempenho nos seguintes casos:  
  
-   Quando ele pode ser garantido que nenhuma outra transação existe que pode interferir em transações de um aplicativo. Essa situação ocorre somente em circunstâncias limitadas, como quando uma pessoa em uma pequena empresa mantém arquivos dBASE que contêm dados de equipe em um computador e não compartilha esses arquivos.  
  
-   Quando a velocidade é mais importante do que a precisão e quaisquer erros provavelmente serão pequenas. Por exemplo, suponha que uma empresa faz muitas vendas de pequeno e que as vendas grandes são raras. Uma transação que estima o valor total de todas as vendas pode usar com segurança o nível de isolamento Read Uncommitted. Embora a transação incluiria os pedidos que estão sendo abertos ou fechados e subsequentemente revertida, eles seriam geralmente cancelar um ao outro e a transação ser muito mais rápida porque não está bloqueado toda vez que ele encontra tal um pedido.  
  
 Para obter mais informações, consulte [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
