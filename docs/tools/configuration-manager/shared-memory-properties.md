---
title: Propriedades de memória compartilhada | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: d02082b26668eabae56ba8e50e4f8a3369d183b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778404"
---
# <a name="shared-memory-properties"></a>Propriedades da memória compartilhada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use a página **Protocolo** na caixa de diálogo **Propriedades de Memória Compartilhada** para habilitar ou desabilitar o protocolo de memória compartilhada. A memória compartilhada é o protocolo mais simples de usar e não precisa de configurações. Como os clientes que usam o protocolo de memória compartilhada só podem se conectar a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada no mesmo computador, ele não é útil para a maior parte da atividade de banco de dados. Use o protocolo de memória compartilhada para solucionar problemas quando você suspeitar que outros protocolos estejam configurados incorretamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser reiniciado para habilitar ou desabilitar o protocolo.  
  
## <a name="options"></a>Opções  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**. O protocolo de memória compartilhada é desabilitado por padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
