---
title: Distributed Replay a configuração do cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3eb00922b4f6e21dd4cfc8a46d8c0c27ed9a5be1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095483"
---
# <a name="distributed-replay-client-configuration"></a>Configuração do Distributed Replay Client
  Use a página **Configuração do Distributed Replay Client** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar os usuários aos quais você deseja conceder permissões administrativas para o serviço Distributed Replay Client.  
  
 Usuários que têm permissões administrativas terão acesso ilimitado ao serviço Distributed Replay Client.  
  
## <a name="options"></a>Opções  
 **Nome do Controlador**  
 Esse é um parâmetro opcional, e o valor padrão é \< *em branco*>.  
  
 Digite o nome do controlador com o qual o computador cliente se comunicará para o serviço Distributed Replay Client. Observe o seguinte:  
  
-   O nome deve ser um FQDN (nome de domínio totalmente qualificado). Por exemplo, um host chamado server1 na hierarquia de produtos na Microsoft pode ter um FQDN de server1.products.microsoft.com.  
  
-   Se você já tiver configurado um controlador, digite o nome do controlador enquanto configura cada cliente.  
  
-   Se você ainda não tiver configurado um controlador, poderá deixar o nome do controlador em branco. No entanto, digite manualmente o nome do controlador no arquivo de **configuração do cliente** .  
  
 **Diretório de trabalho**  
 Especifique o diretório de trabalho para o serviço Distributed Replay Client.  
  
 O diretório de trabalho padrão \<é a *letra da unidade*>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:\\\Program Files \DReplayClient\WorkingDir.  
  
 **Diretório de Resultado**  
 Especifique o diretório de resultado para o serviço Distributed Replay Client.  
  
 O diretório de resultado padrão \<é a *letra da unidade*>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:\\\Program Files \DReplayClient\ResultDir.  
  
  
