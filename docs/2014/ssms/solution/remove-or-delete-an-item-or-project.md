---
title: Remover ou excluir um item ou projeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7834be297cef98d18f78d74999750bf347454bb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118777"
---
# <a name="remove-or-delete-an-item-or-project"></a>Remover ou excluir um item ou projeto
  Os itens de projeto do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são consultas, conexões e arquivos diversos. Você pode remover consultas de projeto e arquivos diversos de sua solução sem apagar os arquivos do armazenamento. Remova um projeto ou item quando não for útil na solução atual, mas que você deseja incluí-lo em outra solução.  
  
### <a name="to-remove-a-project-item"></a>Para remover um item de projeto  
  
1.  No Gerenciador de Soluções, selecione o item de projeto que você deseja remover.  
  
2.  No menu **Editar** , clique em **Remover**.  
  
3.  Na caixa de diálogo de confirmação, clique em **Remover** para remover o item do projeto.  
  
 Um item removido continua existindo no sistema de arquivos. Desta forma, você pode adicionar um item removido à solução original ou a outra solução.  
  
#### <a name="to-remove-a-project"></a>Para remover um projeto  
  
1.  No Gerenciador de Soluções, selecione o projeto que você deseja remover.  
  
2.  No menu **Editar** , clique em **Remover**.  
  
3.  Na caixa de diálogo de confirmação, clique em **OK**para remover o projeto da solução.  
  
 Você pode excluir um projeto permanentemente, mas primeiro é necessário remover qualquer referência ao projeto das soluções do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e depois usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Explorer para excluir os arquivos associados permanentemente do armazenamento.  
  
#### <a name="to-delete-a-project"></a>Para excluir um projeto  
  
1.  No Gerenciador de Soluções, remova o projeto que você deseja excluir da solução.  
  
2.  No Windows Explorer, localize e selecione os arquivos associados ao projeto ou ao item que você deseja excluir.  
  
3.  No menu **Arquivo** , clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de soluções](solution-explorer.md)   
 [Adicionar novos itens a um projeto](add-new-items-to-a-project.md)   
 [Adicionar itens existentes a um projeto](add-existing-items-to-a-project.md)  
  
  