---
title: "Propriedades de memória compartilhada | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: "21"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55c0140b55d4a338ead968e5442316d9a9d130cd
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="shared-memory-properties"></a>Propriedades da memória compartilhada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Use o **protocolo**página o **propriedades de memória compartilhada** caixa de diálogo para habilitar ou desabilitar o protocolo de memória compartilhada. A memória compartilhada é o protocolo mais simples de usar e não precisa de configurações. Como os clientes que usam o protocolo de memória compartilhada só podem se conectar a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada no mesmo computador, ele não é útil para a maior parte da atividade de banco de dados. Use o protocolo de memória compartilhada para solucionar problemas quando você suspeitar que outros protocolos estejam configurados incorretamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]deve ser reiniciado para habilitar ou desabilitar o protocolo.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**. O protocolo de memória compartilhada é desabilitado por padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo um protocolo de rede](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Criando uma cadeia de Conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
