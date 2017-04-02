---
title: "Propriedades da mem&#243;ria compartilhada | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "memória compartilhada [SQL Server]"
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Propriedades da mem&#243;ria compartilhada
  Use a página **Protocolo** na caixa de diálogo **Propriedades de Memória Compartilhada** para habilitar ou desabilitar o protocolo de memória compartilhada. A memória compartilhada é o protocolo mais simples de usar e não precisa de configurações. Como os clientes que usam o protocolo de memória compartilhada só podem se conectar a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada no mesmo computador, ele não é útil para a maior parte da atividade de banco de dados. Use o protocolo de memória compartilhada para solucionar problemas quando você suspeitar que outros protocolos estejam configurados incorretamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser reiniciado para habilitar ou desabilitar o protocolo.  
  
## Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**. O protocolo de memória compartilhada é desabilitado por padrão.  
  
## Consulte também  
 [Escolhendo um protocolo de rede](../Topic/Choosing%20a%20Network%20Protocol.md)   
 [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  