---
title: Remover ou excluir um item ou projeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96e5484ed59b0852f0099602b5a4e3ff359d1b6f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33042383"
---
# <a name="remove-or-delete-an-item-or-project"></a>Remover ou excluir um item ou projeto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Os itens de projeto do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] são consultas, conexões e arquivos diversos. Você pode remover consultas de projeto e arquivos diversos de sua solução sem apagar os arquivos do armazenamento. Remova um projeto ou item quando não for útil na solução atual, mas que você deseja incluí-lo em outra solução.  
  
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
  
