---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5a451792e9732bf00e7bf68ce93b42c99b06fa2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62912402"
---
# <a name="mssqlserver-2"></a>MSSQLSERVER_-2
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|-2|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Tempo limite esgotado.  O período de tempo limite acabou antes de conclusão da operação ou o servidor não está respondendo. (Microsoft SQL Server, Erro: -2)|   
  
## <a name="explanation"></a>Explicação  
 O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Este erro pode ter ocorrido porque o firewall no servidor recusou a conexão. 
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se você configurou o firewall na instância do servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aceitar conexões.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o Firewall do Windows para permitir o acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)   
 [Configurar um Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuração de rede do cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar ou desabilitar um protocolo de rede do servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
