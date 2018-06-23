---
title: Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ff5209c288a38c45f5f6bcea60acdfbf3a45cd78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115558"
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada
  As conexões com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um cliente executado no mesmo computador usam o protocolo de memória compartilhada. A memória compartilhada não tem propriedades configuráveis. Essa memória sempre é tentada primeiro e não pode ser movida da posição superior da lista **Protocolos Habilitados** na lista **Propriedades de Protocolos de Cliente** . O protocolo de Memória Compartilhada pode ser desabilitado, o que é útil ao solucionar problemas dos outros protocolos.  
  
 Não é possível criar um alias usando o protocolo de memória compartilhada, mas se a memória compartilhada estiver habilitada, a conexão com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pelo nome criará uma conexão de memória compartilhada. Uma cadeia de conexão de memória compartilhada usa o formato `lpc:<servername>[\instancename]`.  
  
## <a name="connecting-to-the-local-server"></a>Conectando-se ao servidor local  
 Ao conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no mesmo computador que o cliente, você pode usar **(local)** como o nome do servidor. Esse procedimento não é incentivado, pois leva a ambiguidade. No entanto, ele pode ser útil quando se sabe que o cliente está sendo executado no computador pretendido. Por exemplo, ao criar um aplicativo para usuários móveis desconectados, como uma força de vendas, em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado em computadores laptop e armazenará dados de projeto, um cliente conectado a **(local)** sempre se conectaria ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no laptop. A palavra **localhost** ou um ponto (**.**) pode ser usado em lugar de **(local)**.  
  
## <a name="verifying-your-connection-protocol"></a>Verificando o protocolo de conexão  
 A consulta a seguir retornará o protocolo usado para a conexão atual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Exemplos:  
 Os seguintes nomes se conectarão ao computador local com o protocolo da memória compartilhada, se ele estiver habilitado:  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 Não é possível criar um alias para uma conexão de memória compartilhada.  
  
> [!NOTE]  
>  A especificação de um Endereço IP na caixa **Servidor** resultará em uma conexão TCP/IP.  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma cadeia de conexão válida usando TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Criando uma cadeia de conexão válida usando pipes nomeados](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  