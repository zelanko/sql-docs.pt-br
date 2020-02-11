---
title: Alterar conexões de controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d57f5938cb888a955645f5a9e0b01eeacfc1142b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812785"
---
# <a name="change-source-control-connections"></a>Alterar conexões de controle do código-fonte
  A primeira vez que você adiciona ou abre uma solução de controle do código-fonte, seu provedor cria uma associação entre a pasta raiz do diretório da solução local e a pasta do servidor correspondente.  
  
 A pasta raiz (também chamada de raiz unificada) reside no cliente. Ela é a pasta abaixo da qual podem ser encontrados todos os arquivos referenciados por uma solução ou um projeto. Para encontrar a versão mais recente de uma solução, seu histórico e suas informações de status, localize a pasta do servidor que reside no servidor de controle do código-fonte. No [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, as pastas do servidor são chamadas de projetos.  
  
 Em muitas situações, você precisa desassociar ou desconectar uma solução de sua pasta do servidor. Por exemplo, se o computador em que o provedor de controle do código-fonte reside estiver indisponível, você poderá fazer a conexão com um computador de backup, associar novamente sua solução a uma pasta do servidor salva e retomar o trabalho normalmente. Além disso, se um projeto de controle do código-fonte estiver bifurcado, você poderá ter que associar sua solução à pasta do servidor em que a nova versão de projeto reside.  
  
 Use a interface de usuário do provedor de controle do código-fonte para alterar a pasta do servidor a que a solução está associada. É possível abrir a interface de usuário de controle do código-fonte no ambiente do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>Para abrir a interface de usuário de controle do código-fonte do ambiente do Studio  
  
1.  No menu **arquivo** , aponte para **controle do código-fonte**e clique em **iniciar o Microsoft Visual SourceSafe**.  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas do controle do código-fonte](../../2014/database-engine/source-control-basics.md)   
 [Definir opções de controle do código-fonte](../../2014/database-engine/set-source-control-options.md)   
 [Excluir arquivos do controle do código-fonte](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
