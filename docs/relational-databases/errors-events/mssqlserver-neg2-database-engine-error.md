---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "-2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b6b67d08a3f8beb88d44499c4b3975d88038feb4
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

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
[Configurar o Firewall do Windows para permitir acesso ao SQL Server](~/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolos de rede e bibliotecas de rede](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuração de rede de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar ou desabilitar um protocolo de rede do servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

