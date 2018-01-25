---
title: Remover ou excluir um item ou projeto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-solutions
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 260005349211feaeb74280a65e1b5d89ef092426
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="remove-or-delete-an-item-or-project"></a>Remover ou excluir um item ou projeto
Os itens de projeto [!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] em projetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] são Consultas, Conexões e arquivos Diversos. Você pode remover consultas de projeto e arquivos diversos de sua solução sem apagar os arquivos do armazenamento. Remova um projeto ou item quando não for útil na solução atual, mas que você deseja incluí-lo em outra solução.  
  
### <a name="to-remove-a-project-item"></a>Para remover um item de projeto  
  
1.  No Gerenciador de Soluções, selecione o item de projeto que você deseja remover.  
  
2.  No menu **Editar** , clique em **Remover**.  
  
3.  Na caixa de diálogo de confirmação, clique em **Remover** para remover o item do projeto.  
  
Um item removido continua existindo no sistema de arquivos. Desta forma, você pode adicionar um item removido à solução original ou a outra solução.  
  
#### <a name="to-remove-a-project"></a>Para remover um projeto  
  
1.  No Gerenciador de Soluções, selecione o projeto que você deseja remover.  
  
2.  No menu **Editar** , clique em **Remover**.  
  
3.  Na caixa de diálogo de confirmação, clique em **OK**para remover o projeto da solução.  
  
Você pode excluir um projeto permanentemente, mas primeiro é necessário remover qualquer referência ao projeto das soluções do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] e depois usar o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Explorer para excluir os arquivos associados permanentemente do armazenamento.  
  
#### <a name="to-delete-a-project"></a>Para excluir um projeto  
  
1.  No Gerenciador de Soluções, remova o projeto que você deseja excluir da solução.  
  
2.  No Windows Explorer, localize e selecione os arquivos associados ao projeto ou ao item que você deseja excluir.  
  
3.  No menu **Arquivo** , clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Adicionar novos itens a um projeto](../../ssms/solution/add-new-items-to-a-project.md)  
[Adicionar itens existentes a um projeto](../../ssms/solution/add-existing-items-to-a-project.md)  
  
