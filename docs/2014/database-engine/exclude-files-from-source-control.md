---
title: Excluir arquivos do controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42ae16970e59e2eac1af68e54a38b19bd760c068
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779896"
---
# <a name="exclude-files-from-source-control"></a>Excluir arquivos do controle do código-fonte
  Se a solução na qual você está trabalhando contiver arquivos que não exigem serviços de controle do código-fonte, você poderá usar o comando **excluir do controle do código-fonte** para excluir o arquivo do controle do código-fonte. Quando você faz isso, o arquivo permanece no banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, mas já não é feito o check-in ou check-out com o projeto.  
  
 Você deve usar o comando **excluir do controle do código-fonte** somente em arquivos gerados. Um arquivo gerado é aquele que pode ser totalmente recriado [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] com base no conteúdo de outro arquivo na solução.  
  
### <a name="to-exclude-a-file-from-source-control"></a>Para excluir arquivos do controle de código-fonte  
  
1.  No Gerenciador de Soluções, selecione o arquivo que irá excluir.  
  
2.  No menu **arquivo** , aponte para **controle do código-fonte**e clique em **excluir** * \<nome do arquivo>* **do controle do código-fonte**.  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas do controle do código-fonte](../../2014/database-engine/source-control-basics.md)   
 [Definir opções de controle do código-fonte](../../2014/database-engine/set-source-control-options.md)   
 [Alterar conexões de controle do código-fonte](../../2014/database-engine/change-source-control-connections.md)  
  
  
