---
title: "Gerenciando o tamanho de transação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b333a2aa36c2dd7f2cd0e0065a955455549a813e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="managing-transaction-size"></a>Gerenciando o tamanho da transação
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Durante o trabalho com transações, é importante manter as transações com a maior brevidade possível. O modo padrão de confirmação automática, que você pode habilitar ou desabilitar usando o [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) método, confirmará todas as ações para você. Trata-se do modo mais fácil de trabalhar com a maioria dos desenvolvedores.  
  
 Ao usar transações manuais, certifique-se de que o código confirme a transação o mais rápido possível. A manutenção de uma transação em aberto impede outros usuários de acessarem os dados. Por exemplo, uma boa prática de programação pode ser colocar uma chamada de retorno no bloco catch e uma chamada de confirmação no bloco final. No entanto, isso depende do design do aplicativo.  
  
 A manutenção do tamanho menor das transações cria uma simultaneidade melhor. Por exemplo, se iniciar uma transação manual e modificar 10.000 linhas em uma tabela de 20.000 linhas, você terá metade da tabela completamente bloqueada para todos os outros usuários, mesmo que eles só estejam lendo os dados. A redução das modificações para 2.000 linhas disponibiliza 90 por cento da tabela.  
  
 Além disso, use a configuração de tempo limite de bloqueio se o aplicativo espera algum problema de bloqueio e precisa expirar. Você pode fazer isso usando o [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) método. O padrão do tempo limite é -1, o que significa que ele será bloqueado indefinidamente enquanto aguarda o bloqueio. É possível definir o tempo limite de bloqueio para 30 segundos, o que levará a conexão bloqueada expirar em 30 segundos se houver bloqueio por outra conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

