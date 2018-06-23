---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c1aac9c0f586e12fd555b675a95c7936a6077b42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006845"
---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|233|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Uma conexão com o servidor foi estabelecida com êxito, mas ocorreu um erro durante o processo de logon. (provedor: Provedor de Memória Compartilhada, erro: 0 – Nenhum processo está na outra extremidade do pipe.) (Microsoft SQL Server, Erro: 233)|  
  
## <a name="explanation"></a>Explicação  
 O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Esse erro pode ocorrer porque o servidor não está configurado para aceitar conexões remotas.  
  
## <a name="user-action"></a>Ação do usuário  
 Use a ferramenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceite conexões remotas.  
  
## <a name="see-also"></a>Consulte também  
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuração de rede do cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar ou desabilitar um protocolo de rede do servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  