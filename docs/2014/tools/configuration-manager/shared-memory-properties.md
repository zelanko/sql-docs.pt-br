---
title: Propriedades da memória compartilhada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bea56ada3ef490225fd08892128abb482b9342a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62999534"
---
# <a name="shared-memory-properties"></a>Propriedades da memória compartilhada
  Use a página **Protocolo**na caixa de diálogo **Propriedades de Memória Compartilhada** para habilitar ou desabilitar o protocolo de memória compartilhada. A memória compartilhada é o protocolo mais simples de usar e não precisa de configurações. Como os clientes que usam o protocolo de memória compartilhada só podem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectar a uma instância em execução no mesmo computador, ele não é útil para a maioria das atividades do banco de dados. Use o protocolo de memória compartilhada para solucionar problemas quando você suspeitar que outros protocolos estejam configurados incorretamente.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser reiniciado para habilitar ou desabilitar o protocolo.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**. O protocolo de memória compartilhada é desabilitado por padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
