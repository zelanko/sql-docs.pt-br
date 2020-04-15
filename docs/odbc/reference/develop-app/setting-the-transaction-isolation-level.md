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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299806"
---
# <a name="setting-the-transaction-isolation-level"></a>Configurar o nível de isolamento da transação
Para definir o nível de isolamento da transação, um aplicativo usa o atributo de conexão SQL_ATTR_TXN_ISOLATION. Se a fonte de dados não suportar o nível de isolamento solicitado, o driver ou a fonte de dados podem definir um nível mais alto. Para determinar quais níveis de isolamento de transações uma fonte de dados suporta e qual é o nível de isolamento padrão, um aplicativo chama **sqlGetInfo** com as opções de SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Níveis mais altos de isolamento de transações oferecem a maior proteção para a integridade dos dados do banco de dados. As transações serializáveis são garantidas como não afetadas por outras transações e, portanto, garantidas para manter a integridade do banco de dados.  
  
 No entanto, um nível mais alto de isolamento de transações pode causar um desempenho mais lento, pois aumenta as chances de que o aplicativo tenha que esperar que os bloqueios de dados sejam liberados. Um aplicativo pode especificar um nível mais baixo de isolamento para aumentar o desempenho nos seguintes casos:  
  
-   Quando pode ser garantido que não existam outras transações que possam interferir com as transações de um aplicativo. Essa situação ocorre apenas em circunstâncias limitadas, como quando uma pessoa em uma pequena empresa mantém arquivos dBASE que contêm dados pessoais em um computador e não compartilham esses arquivos.  
  
-   Quando a velocidade é mais crítica do que a precisão e qualquer erro é provável que seja pequeno. Por exemplo, suponha que uma empresa faça muitas vendas pequenas e que grandes vendas são raras. Uma transação que estima o valor total de todas as vendas abertas pode usar com segurança o nível de isolamento Read Uncommitted. Embora a transação inclua pedidos que estão sendo abertos ou fechados e são posteriormente revertidos, estes geralmente se cancelariam e a transação seria muito mais rápida porque não é bloqueada toda vez que encontra tal pedido.  
  
 Para obter mais informações, consulte [Optimistic Concurrency](../../../odbc/reference/develop-app/optimistic-concurrency.md).
