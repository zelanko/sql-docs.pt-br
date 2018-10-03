---
title: Instalar o Distributed Replay usando um arquivo de configuração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a1ba661a0a00931f52aa7d38cc8d96730c685fa7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078306"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>Instalar o Distributed Replay usando um arquivo de configuração
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece a capacidade de gerar um arquivo de configuração baseado na entrada do usuário e nos padrões do sistema. Se você especificar que deseja instalar as ferramentas de Gerenciamento, poderá usar o arquivo de configuração para implantar os três componentes de Distributed Replay (Ferramenta de Administração, Distributed Replay Controller e Distributed Replay Client). Há suporte para a Instalação, reparo e desinstalação dos componentes do Distributed Replay.  
  
 A Instalação dá suporte ao uso do arquivo de configuração apenas por meio da linha de comando. A ordem de processamento dos parâmetros ao usar o arquivo de configuração é descrita a seguir:  
  
-   O arquivo de configuração substitui os padrões em um pacote  
  
-   Os valores da linha de comando substituem os valores do arquivo de configuração  
  
 Para obter mais informações sobre como usar um arquivo de configuração, consulte [instalar o SQL Server 2014 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).  
  
> [!IMPORTANT]  
>  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
### <a name="to-generate-a-configuration-file"></a>Para gerar um arquivo de configuração  
  
1.  Siga o Assistente de Instalação até a página **Pronto para Instalar** . O caminho para o arquivo de configuração é especificado na página **Pronto para Instalar** na seção do caminho do arquivo de configuração.  
  
2.  Cancele a instalação sem realmente concluí-la para gerar o arquivo INI.  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>Para instalar o Distributed Replay usando o arquivo de configuração  
  
-   Execute a instalação no prompt de comando e forneça o ConfigurationFile.ini por meio do parâmetro ConfigurationFile.  
  
 **Sintaxe de exemplo**  
  
 O seguinte é um exemplo de como especificar o arquivo de configuração no prompt de comando:  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  Você deve especificar as duas senhas na linha de comando, porque não é possível configurá-las no arquivo de configuração.  
  
  
