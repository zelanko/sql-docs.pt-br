---
title: Concluir as etapas pós-instalação
titleSuffix: SQL Server Distributed Replay
description: Depois de instalar o Distributed Replay, modifique as contas de serviço do cliente e do controlador do Distributed Replay.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: bda2bda26d8933c580597b01fba79d1912cb5b56
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85681855"
---
# <a name="complete-the-post-installation-steps"></a>Concluir as etapas de pós-instalação

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Depois de instalar o Distributed Replay, modifique as contas de serviços cliente e controlador do Distributed Replay.  
  
## <a name="to-complete-the-post-installation-steps"></a>Para concluir as etapas de pós-instalação  
  
1. **Criar regras de firewall**: no controlador e nos computadores cliente, você deve permitir tráfego de entrada pelo firewall para o serviço correspondente. Especifique as regras de firewall para os executáveis de serviço, localizados nas pastas de instalação.  
  
    1. Para o serviço de controlador, crie uma regra para **DReplayController.exe**, localizado na pasta de instalação. Por exemplo, o comando a seguir habilita essa regra, onde `%InstallPath%` é a pasta de instalação do serviço:  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2. Para o serviço de cliente, em cada computador cliente, crie uma regra para **DReplayClient.exe**, localizado na pasta de instalação. Por exemplo, o comando a seguir habilita essa regra, onde `%InstallPath%` é a pasta de instalação do serviço:  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2. **Conceder permissões a cada cliente no servidor alvo**: depois de concluir a instalação do serviço de cliente nos computadores cliente, adicione manualmente as contas de serviço de cliente à função sysadmin na instância alvo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework

Você deve ter permissões administrativas para instalar qualquer recurso do Distributed Replay. Apenas um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissões sysadmin pode adicionar as contas de serviço de cliente à função de servidor sysadmin do servidor de teste. Para obter mais informações sobre as considerações de segurança do Distributed Replay, veja [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).