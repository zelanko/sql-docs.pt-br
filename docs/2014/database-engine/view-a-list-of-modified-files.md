---
title: Exibir uma lista de arquivos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9f500eb460cab8734a062ddf6561cbdf01d0f773
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927567"
---
# <a name="view-a-list-of-modified-files"></a>Exibir uma lista de arquivos modificados
  Você pode usar a janela **check-ins pendentes** para exibir sempre uma lista dos arquivos com check-out na solução atual e fazer check-in desses arquivos com um único clique de botão.  
  
### <a name="to-view-a-list-of-modified-files"></a>Para exibir uma lista de arquivos modificados  
  
1.  No menu **Exibir** , clique em **check-ins pendentes**.  
  
2.  Para fazer check-in nos arquivos selecionados, clique em **fazer check-in**. Como alternativa, você pode encaixar a janela **check-ins pendentes** no lado direito do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ambiente para que você possa fazer check-in nos arquivos quando terminar de trabalhar.  
  
     **Fazer Check-in**  
     Faz o check-in na solução.  
  
     **Comentários**  
     Associa um comentário de texto sem-formatação ao check-in pendente. É criado um comentário e associado a cada versão de um projeto e armazenado no banco de dados de controle de código-fonte.  
  
     **Opções**  
     Especifica as ações que o controle do código-fonte deve tomar quando você clica no botão **check-in** .  
  
    -   **Mantenha Todos Check-out**  
  
         Especifica que suas alterações devem ser gravadas no provedor do controle do código-fonte mas que os arquivos devem permanecer check-out.  
  
     **Classificar**  
     Especifica a ordem de classificação para as colunas exibidas na lista Itens.  
  
     **Colunas**  
     Exibe uma lista das colunas que você pode adicionar à lista Itens da janela.  
  
     **Exibição de árvore**  
     Exibe a hierarquia da pasta e do arquivo para a solução ou projeto que você está fazendo o check-in.  
  
     **Exibição Simples**  
     Exibe os arquivos dos quais está fazendo check-in como listas simples na conexão de controle do código-fonte.  
  
     **Comparar Versões**  
     Abre a caixa de diálogo **Opções de diferenças** do Visual SourceSafe, que compara um arquivo selecionado em seu projeto de ambiente de desenvolvimento com qualquer outro arquivo selecionado e mostra as diferenças, se houver.  
  
     **Desfazer check-out**  
     Reverte o check-out de todos os itens selecionados na janela **check-ins pendentes** .  
  
     **Nome**  
     Exibe uma lista dos itens disponíveis para fazer check-in. Os itens mostram as caixas de seleção ao seu lado selecionadas. Se você não quiser fazer o check-in em um item específico, desmarque a caixa de seleção próxima a ele.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar Check-ins](../../2014/database-engine/manage-checkins.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  
