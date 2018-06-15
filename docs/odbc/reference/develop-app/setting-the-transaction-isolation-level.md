---
title: Configurando o isolamento da transação nível | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8ada820d501d49298cf245cbc88e8fbdfdba331
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912491"
---
# <a name="setting-the-transaction-isolation-level"></a>Configurando o isolamento de transação de nível
Para definir o nível de isolamento da transação, um aplicativo usa o atributo de conexão SQL_ATTR_TXN_ISOLATION. Se a fonte de dados não der suporte para o nível de isolamento solicitado, o driver ou fonte de dados pode definir um nível mais alto. Para determinar os níveis de isolamento da transação que uma fonte de dados oferece suporte e o nível de isolamento padrão é, um aplicativo chama **SQLGetInfo** com as opções SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, respectivamente.  
  
 Níveis mais altos de isolamento da transação oferecem a melhor proteção para a integridade do banco de dados. Transações serializáveis são a garantia de ser afetado por outras transações e, portanto, são garantidas para manter a integridade do banco de dados.  
  
 No entanto, um nível mais alto de isolamento da transação pode causar um desempenho mais lento porque aumenta as chances de que o aplicativo terá que aguardar os bloqueios de dados a ser liberado. Um aplicativo pode especificar um nível inferior de isolamento para aumentar o desempenho nos seguintes casos:  
  
-   Quando pode ser garantido que ele exista nenhuma outra transação que pode interferir em transações de um aplicativo. Essa situação ocorre somente em circunstâncias limitadas, como quando uma pessoa em uma pequena empresa mantém arquivos dBASE que contêm dados de funcionários em um computador e não compartilhe esses arquivos.  
  
-   Quando a velocidade é mais crítica que a precisão e a quaisquer erros têm probabilidade de ser pequeno. Por exemplo, suponha que uma empresa faz vendas pequenas muitas e que as vendas grandes são raras. Uma transação que calcula o valor total de todas as vendas pode usar o nível de isolamento Read Uncommitted com segurança. Embora a transação incluiria pedidos que estão sendo aberto ou fechado e posteriormente revertida, esses geralmente seriam Cancelar uns aos outros e a transação é muito mais rápida porque cada vez que ele encontra esse uma ordem não está bloqueado.  
  
 Para obter mais informações, consulte [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).
