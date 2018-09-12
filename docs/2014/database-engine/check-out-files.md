---
title: Fazer Check-Out de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 313d5d85bd7ad8343fe90f0eeda16bf15e53ef44
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808432"
---
# <a name="check-out-files"></a>Fazer check-out de arquivos
  A menos que você tenha configurado o ambiente do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para permitir a edição de arquivos que tenham feito check-in, faça o check-out de um arquivo antes de modificá-lo. Quando você faz o check-out de um arquivo, uma cópia da versão de arquivo é copiada no disco local e o atributo somente leitura é removido.  
  
 Você pode fazer o check-out de arquivos em modo exclusivo ou compartilhado. Quando você fizer o check-out de um arquivo exclusivamente, nenhum outro usuário poderá fazer o check-out do arquivo até você concluir seu check-out. Quando você faz o check-out de um arquivo no modo compartilhado, outros usuários podem fazer o check-out e modificar o arquivo; talvez seja necessário mesclar a versão de check-out com as versões criadas por outros usuários.  
  
 Use o comando **Check-Out** para fazer o check-out de arquivos e projetos com controle do código-fonte. Se você usar esse comando para fazer o check-out de uma solução ou projeto, todos os arquivos da solução ou do projeto também farão check-out. Entretanto, fazer o check-out de um arquivo do código-fonte individual não resulta no check-out do projeto ou da solução a que ele pertence.  
  
> [!NOTE]  
>  Se o banco de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe do projeto for configurado para permitir vários check-outs e você quiser fazer o check-out de um arquivo exclusivamente, desmarque a opção **Permitir múltiplos check-outs** na caixa de diálogo **Opções Avançadas de Check-Out** antes de fazer o check-out do arquivo. Você deve reiniciar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para que essa configuração entre em vigor.  
  
### <a name="to-check-out-a-file"></a>Para fazer check-out de um arquivo  
  
1.  No Gerenciador de Soluções, selecione o projeto ou o arquivo.  
  
2.  No menu **Arquivo** , aponte para **Controle do Código-Fonte**e clique em **Check-Out para Edição**.  
  
3.  Se a caixa de diálogo **Check-Out para Edição** for exibida, selecione os itens que você deseja e clique em **Check-Out**. Se você tiver configurado o ambiente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para não exibir a caixa de diálogo **Check-out** , os itens selecionados no Gerenciador de Soluções e quaisquer objetos filho que eles possam ter terão check-out imediatamente.  
  
     **Fazer Check-out**  
     Faça check-out de todos os itens selecionados.  
  
     **Colunas**  
     Identifique as colunas a serem exibidas e a ordem em que elas são exibidas.  
  
     **Comentários**  
     Especifique um comentário a ser associado com a operação de check-out.  
  
     **Não mostrar Check-Out caixa de diálogo, ao fazer check-out de itens**  
     Suprima a caixa de diálogo durante operações de check-out.  
  
     **Modo de exibição simples**  
     Exiba os itens de check-out como listas simples em suas conexões de controle do código fonte.  
  
     **Editar**  
     Modifique um item sem fazer seu check-out. O botão **Editar** só será exibido se você tiver o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] configurado para oferecer suporte à edição de arquivos com check-in já feito.  
  
     **Nome**  
     Exibe os nomes dos itens disponíveis para check-out. Os itens selecionados são exibidos com caixas de seleção ao lado. Se não quiser fazer check-out de um item em particular, desmarque sua caixa de seleção.  
  
     **Opções**  
     Exibe opções de check-out específico de plug-ins de controle do código fonte quando a seta à direita do botão é clicada.  
  
     **Sort**  
     Classifique a ordem das colunas exibidas.  
  
     **Exibição de árvore**  
     Exiba a hierarquia de pastas e arquivos do item de check-out.  
  
## <a name="see-also"></a>Consulte também  
 [Editar arquivos com Check-In](../../2014/database-engine/edit-checked-in-files.md)   
 [Check-Out de arquivos na edição automático](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [Desfazer check-outs](../../2014/database-engine/undo-checkouts.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  
