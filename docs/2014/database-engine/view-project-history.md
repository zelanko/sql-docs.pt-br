---
title: Exibir o histórico do projeto | Microsoft Docs
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
- viewing project history
- version control services [SQL Server], project history
- projects [SQL Server Management Studio], historical information
- historical information [SQL Server], projects
ms.assetid: be0ea2ac-4a35-429c-9c9e-4001ea9035a4
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e10e920a5c60d389eaec6a5af06e4597d9667967
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287842"
---
# <a name="view-project-history"></a>Exibir histórico de projetos
  O histórico de um projeto do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe (VSS) inclui uma lista de todas as ações executadas em cada um dos arquivos do projeto, incluindo criação, adição, exclusão e recuperação de arquivos.  
  
> [!NOTE]  
>  Um projeto do Visual SourceSafe normalmente é chamado de pasta do servidor de controle do código-fonte, o local em que a versão do servidor de um arquivo com controle do código-fonte é armazenado no servidor.  
  
 Você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para examinar o histórico do projeto do Visual SourceSafe a que a solução atual pertence. Com base nas informações exibidas como parte do histórico de um projeto, você pode recuperar cópias locais das versões de arquivo, restaurar versões excluídas ou compartilhar uma versão de arquivo entre projetos.  
  
### <a name="to-view-the-history-of-a-vss-project"></a>Para exibir o histórico de um projeto do VSS  
  
1.  No Gerenciador de Soluções, selecione o projeto.  
  
2.  Sobre o **arquivo** , aponte para **controle do código-fonte** e clique em **Exibir histórico**.  
  
3.  No **histórico de** \<projeto > caixa de diálogo caixa, execute uma das seguintes ações:  
  
    -   Exiba a cópia do sistema de controle do código-fonte de um arquivo selecionado.  
  
    -   Exiba as informações detalhadas de um arquivo selecionado.  
  
    -   Recupere um arquivo selecionado para o disco local.  
  
    -   Faça o check-out de um arquivo selecionado.  
  
    -   Compartilhe um arquivo selecionado entre dois projetos de controle do código-fonte.  
  
    -   Exporte o relatório de histórico para uma impressora, um arquivo ou para a área de transferência.  
  
## <a name="see-also"></a>Consulte também  
 [Definir e recuperar informações de versão](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [Exibir o Status do arquivo](../../2014/database-engine/view-file-status.md)   
 [Recuperar arquivos](../../2014/database-engine/retrieve-files.md)   
 [Comparar arquivos](../../2014/database-engine/compare-files.md)  
  
  
