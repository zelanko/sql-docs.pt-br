---
title: Gerenciando o tamanho da transação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e53ab6e5f2fc2cc12db37d81b1c8f687b503158
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956351"
---
# <a name="managing-transaction-size"></a>Gerenciando o tamanho da transação
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Durante o trabalho com transações, é importante manter as transações com a maior brevidade possível. O modo padrão de confirmação automática, que é possível habilitar ou desabilitar usando-se o método [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), confirmará todas as ações para você. Trata-se do modo mais fácil de trabalhar com a maioria dos desenvolvedores.  
  
 Ao usar transações manuais, certifique-se de que o código confirme a transação o mais rápido possível. A manutenção de uma transação em aberto impede outros usuários de acessarem os dados. Por exemplo, uma boa prática de programação pode ser colocar uma chamada de retorno no bloco catch e uma chamada de confirmação no bloco final. No entanto, isso depende do design do aplicativo.  
  
 A manutenção do tamanho menor das transações cria uma simultaneidade melhor. Por exemplo, se iniciar uma transação manual e modificar 10.000 linhas em uma tabela de 20.000 linhas, você terá metade da tabela completamente bloqueada para todos os outros usuários, mesmo que eles só estejam lendo os dados. A redução das modificações para 2.000 linhas disponibiliza 90 por cento da tabela.  
  
 Além disso, use a configuração de tempo limite de bloqueio se o aplicativo espera algum problema de bloqueio e precisa expirar. É possível fazer isso usando-se o método [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md). O padrão do tempo limite é -1, o que significa que ele será bloqueado indefinidamente enquanto aguarda o bloqueio. É possível definir o tempo limite de bloqueio para 30 segundos, o que levará a conexão bloqueada expirar em 30 segundos se houver bloqueio por outra conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
