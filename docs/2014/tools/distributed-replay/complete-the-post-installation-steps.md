---
title: Concluir as etapas pós-instalação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 558236f7034588a544aa4fb78091c19475cc8f4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63025657"
---
# <a name="complete-the-post-installation-steps"></a>Concluir as etapas de pós-instalação
  Depois de instalar o Distributed Replay, modifique as contas de serviços cliente e controlador do Distributed Replay.  
  
### <a name="to-complete-the-post-installation-steps"></a>Para concluir as etapas de pós-instalação  
  
1.  **Crie regras de firewall**: no controlador e nos computadores cliente, você deve permitir tráfego de entrada pelo firewall para o serviço correspondente. Especifique as regras de firewall para os executáveis de serviço, localizados nas pastas de instalação.  
  
    1.  Para o serviço de controlador, crie uma regra para **DReplayController.exe**, localizado na pasta de instalação. Por exemplo, o comando a seguir habilita essa regra, onde `%InstallPath%` é a pasta de instalação do serviço:  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  Para o serviço de cliente, em cada computador cliente, crie uma regra para **DReplayClient.exe**, localizado na pasta de instalação. Por exemplo, o comando a seguir habilita essa regra, onde `%InstallPath%` é a pasta de instalação do serviço:  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **Conceda permissões a cada cliente no servidor de destino**: Depois de concluir a instalação do serviço de cliente nos computadores cliente, adicione manualmente as contas de serviço de cliente à função sysadmin na instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter permissões administrativas para instalar qualquer recurso do Distributed Replay. Apenas um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha permissões sysadmin pode adicionar as contas de serviço de cliente à função de servidor sysadmin do servidor de teste. Para obter mais informações sobre as considerações de segurança do Distributed Replay, veja [Segurança do Distributed Replay](distributed-replay-security.md).  
  
  
