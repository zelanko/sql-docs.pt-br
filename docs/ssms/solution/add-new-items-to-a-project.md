---
title: Adicionar novos itens a um projeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 76af8692-324f-4f5e-b1a0-d72ca8a107e3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fcb6d5e1a811f13a346a3daf89de459273cd2140
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105345"
---
# <a name="add-new-items-to-a-project"></a>Adicionar novos itens a um projeto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Adicione novos itens a um projeto para estender a funcionalidade do aplicativo. Um novo item pode ser uma consulta ou uma conexão. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem dois tipos de projeto: Projeto de Script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Projeto de Script do Analysis Services. O tipo de projeto determina os itens que você pode adicionar ao projeto. Por exemplo, você pode adicionar uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] (um arquivo com uma extensão .sql) a um projeto de script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não pode adicioná-lo a um Projeto de Script do Analysis Services.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não permite a criação de pastas dentro de projetos. Para organizar seu trabalho, crie vários projetos dentro da solução.  
  
### <a name="to-add-a-new-query-to-an-existing-project"></a>Para adicionar uma nova consulta a um projeto existente  
  
1.  No Gerenciador de Soluções, selecione um projeto de destino.  
  
2.  No menu **Projeto** , clique em **Adicionar Novo Item**.  
  
3.  Na caixa de diálogo **Adicionar Novo Item** , selecione uma categoria no painel esquerdo.  
  
4.  Selecione um modelo de consulta no painel direito e clique em **Adicionar**. A nova consulta é adicionada à pasta **Consultas** do projeto.  
  
5.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados** , especifique uma conexão para a nova consulta e clique em **Conectar**. Você poderá clicar em **Cancelar** na caixa de diálogo da conexão se não quiser associar uma conexão com a consulta nova.  
  
6.  Caso deseje, renomeie a consulta no Gerenciador de Soluções.  
  
### <a name="to-add-a-new-connection-to-an-existing-project"></a>Para adicionar uma nova conexão a um projeto existente  
  
1.  No Gerenciador de Soluções, selecione um projeto de destino.  
  
2.  No menu **Projeto** , clique em **Adicionar Novo Item**.  
  
3.  Selecione **Conexão** no painel esquerdo.  
  
4.  Selecione **Nova Conexão** no painel direito e clique em **Adicionar**.  
  
5.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados** , especifique uma conexão para a nova consulta e clique em **Conectar**. A nova conexão é adicionada à pasta **Conexões** do projeto.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Como associar extensões de arquivo a um Editor de Códigos](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
[Adicionar itens existentes a um projeto](../../ssms/solution/add-existing-items-to-a-project.md)  
[Remover ou excluir um item ou projeto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
