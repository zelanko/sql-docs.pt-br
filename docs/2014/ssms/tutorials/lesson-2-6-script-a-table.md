---
title: Gerar script de uma tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7808c9270e0085c2f8fafb5262d6356f8c8d1e08
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196706"
---
# <a name="script-a-table"></a>Gerar script de uma tabela
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode criar scripts para selecionar, inserir, atualizar e excluir tabelas, além de criar, alterar, remover ou executar procedimentos armazenados.  
  
 Às vezes você pode querer um script que tenha várias opções, como remover um procedimento e depois criar um procedimento, ou criar uma tabela e alterá-la. Para criar scripts combinados, salve o primeiro script em uma janela do Editor de Consultas e o segundo na área de transferência para que você possa colá-lo na janela após o primeiro script.  
  
## <a name="creating-an-update-script"></a>Criando um script de atualização  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>Para criar um script de inserção para uma tabela  
  
1.  No Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], **Tabelas**, clique com o botão direito do mouse em **HumanResources.Employee** e aponte para **Criar Script de Tabela Como**.  
  
2.  O menu de atalho tem sete opções de script disponíveis: **CREATE To**, **DROP To**, **DROP e CREATE To**, **SELECT To**, **INSERT To**, **UPDATE To**e **DELETE To**. Aponte para **UPDATE To**e clique em **Nova Janela do Editor de Consultas**.  
  
3.  Uma nova janela do Editor de Consultas é aberta, estabelece uma conexão e apresenta a instrução de atualização inteira.  
  
     Esse exercício demonstra como o recurso de script pode fazer mais do que simplesmente executar o script de criação de uma tabela ou procedimento armazenado. Esse novo recurso pode ajudá-lo a adicionar rapidamente scripts de manipulação de dados a seu projeto e a executar scripts de procedimento armazenados com facilidade. Isso pode economizar tempo em tabelas e procedimentos com muitos campos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Resumo: Gravando Transact-SQL](../../tutorials/summary-writing-transact-sql.md)  
  
  
