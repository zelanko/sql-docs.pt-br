---
title: Excluir arquivos do controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b3507f06db699e8e88de2fe2e22f870b97b896e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330436"
---
# <a name="exclude-files-from-source-control"></a>Excluir arquivos do controle do código-fonte
  Se a solução que você está trabalhando contiver arquivos que não requerem serviços de controle do código-fonte, você pode usar o **excluir do controle do código-fonte** comando para excluir o arquivo de controle de origem. Quando você faz isso, o arquivo permanece no banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, mas já não é feito o check-in ou check-out com o projeto.  
  
 Você deve usar o **excluir do controle do código-fonte** comando apenas em arquivos gerados. Um arquivo gerado é aquele que pode ser completamente recriado pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] com base no conteúdo de outro arquivo na solução.  
  
### <a name="to-exclude-a-file-from-source-control"></a>Para excluir arquivos do controle de código-fonte  
  
1.  No Gerenciador de Soluções, selecione o arquivo que irá excluir.  
  
2.  No **arquivo** , aponte para **controle do código-fonte**e, em seguida, clique em **excluir**  *\<nome do arquivo >* **de Controle de fonte**.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas de controle do código-fonte](../../2014/database-engine/source-control-basics.md)   
 [Definir opções de controle do código-fonte](../../2014/database-engine/set-source-control-options.md)   
 [Alterar conexões de controle do código-fonte](../../2014/database-engine/change-source-control-connections.md)  
  
  
