---
title: MSSQLSERVER_2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- "2"
helpviewer_keywords:
- 2 (Database Engine error)
ms.assetid: 567fb571-7cda-4ce8-a702-cdff2df5d419
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d970b6571456ce5a531a393b3a483d48b24d90d4
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2"></a>MSSQLSERVER_2
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro ao estabelecer uma conexão com o servidor.  Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (provedor: Provedor de Pipes Nomeados, erro: 40 – Não foi possível abrir uma conexão com o SQL Server) (Provedor de Dados do .Net SqlClient)|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não respondeu à solicitação do cliente porque o servidor provavelmente não foi iniciado.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se o servidor está iniciado.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar os serviços do Mecanismo de Banco de Dados](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolos de rede e bibliotecas de rede](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuração de rede de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar ou desabilitar um protocolo de rede do servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
