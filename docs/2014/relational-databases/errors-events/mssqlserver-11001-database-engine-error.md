---
title: MSSQLSERVER_11001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "12001"
helpviewer_keywords:
- 11001 (Database Engine error)
ms.assetid: 53d4d63a-61e3-441f-bfe9-9d44f7a05fd4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7fd68c670d82bf70365f26cc435e66f34d174a79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916159"
---
# <a name="mssqlserver_11001"></a>MSSQLSERVER_11001
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|11001|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro ao estabelecer uma conexão com o servidor.  Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (provedor: Provedor TCP, erro: 0 – Nenhum host desse tipo é conhecido.) (Provedor de Dados .NET SqlClient)|  
  
## <a name="explanation"></a>Explicação  
 O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Esse erro pode ocorrer porque o cliente não pode resolver o nome do servidor ou o nome do servidor está incorreto.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se você digitou o nome correto do servidor no cliente e se é possível resolver o nome do servidor no cliente. Para verificar a resolução de nomes TCP/IP, é possível usar o comando **ping** no sistema operacional Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuração de rede do cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar ou desabilitar um protocolo de rede do servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
