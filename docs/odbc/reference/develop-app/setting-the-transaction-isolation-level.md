---
title: Definindo o nível de isolamento da transação | Microsoft Docs
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
ms.openlocfilehash: e59db823f8b84edfb5c92f2d142c8238449e3323
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107586"
---
# <a name="setting-the-transaction-isolation-level"></a>Configurar o nível de isolamento da transação
Para definir o nível de isolamento da transação, um aplicativo usa o atributo de conexão SQL_ATTR_TXN_ISOLATION. Se a fonte de dados não oferecer suporte ao nível de isolamento solicitado, o driver ou a fonte de dados poderá definir um nível superior. Para determinar quais níveis de isolamento de transação são compatíveis com uma fonte de dados e qual é o nível de isolamento padrão, um aplicativo chama **SQLGetInfo** com as opções SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Níveis mais altos de isolamento de transação oferecem a maior proteção para a integridade dos dados do banco de dados. As transações serializáveis têm garantia de não serem afetadas por outras transações e, portanto, garantem a manutenção da integridade do banco de dados.  
  
 No entanto, um nível mais alto de isolamento de transação pode causar um desempenho mais lento, pois aumenta as chances de que o aplicativo precise aguardar a liberação de bloqueios nos dados. Um aplicativo pode especificar um nível inferior de isolamento para aumentar o desempenho nos seguintes casos:  
  
-   Quando pode ser garantido que não existam outras transações que possam interferir nas transações de um aplicativo. Essa situação ocorre apenas em circunstâncias limitadas, como quando uma pessoa em uma empresa pequena mantém arquivos do dBASE que contêm dados de pessoal em um computador e não compartilha esses arquivos.  
  
-   Quando a velocidade é mais crítica do que a precisão e os erros provavelmente serão pequenos. Por exemplo, suponha que uma empresa faça muitas pequenas vendas e que grandes vendas sejam raras. Uma transação que estima o valor total de todas as vendas abertas pode usar com segurança o nível de isolamento de leitura não confirmada. Embora a transação inclua pedidos que estão sendo abertos ou fechados e, subsequentemente, sejam revertidas, isso geralmente cancelaria um ao outro e a transação seria muito mais rápida porque não é bloqueada toda vez que encontra tal ordem.  
  
 Para obter mais informações, consulte [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
