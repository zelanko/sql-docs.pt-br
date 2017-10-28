---
title: Criar scripts usando modelos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 827475f33c02147c2bf6d6b73263fc8aed7b6d47
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="lesson-3-1---create-scripts-using-templates"></a>Lição 3-1 – Criar scripts usando modelos
O Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um grande número de modelos de script que contêm as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para muitas tarefas comuns. Esses modelos contêm parâmetros para obter os valores fornecidos pelo usuário, como um nome de tabela. Usando os parâmetros, você pode digitar o nome uma vez e depois copiar automaticamente o nome em todos os locais necessários dentro do script. Você pode escrever seus próprios modelos personalizados para oferecer suporte aos scripts escritos com frequência. Também é possível reorganizar a árvore de modelo, movendo modelos ou criando pastas novas para armazenar os modelos. No procedimento a seguir, você usará um modelo para criar um banco de dados, especificando o modelo de agrupamento.  
  
## <a name="using-templates"></a>Usando modelos  
  
#### <a name="to-create-a-script-using-a-template"></a>Para criar um script usando um modelo  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  Os modelos do Explorador de Modelos são organizados em grupos. Expanda **Banco de Dados**e clique duas vezes em **Criar Banco de Dados**.  
  
3.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados** , complete as informações de conexão e clique em **Conectar**. Uma nova janela do Editor de Consultas será aberta, exibindo o conteúdo do modelo **Criar Banco de Dados** .  
  
4.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**.  
  
5.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , a coluna **Valor** contém um valor sugerido para o parâmetro **Database_Name** . No caixa de parâmetro **Nome do Banco de Dados** , digite **Marketing**e clique em **OK**. Observe que "Marketing" é inserido no script em vários locais.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Criar modelos personalizados](../../tools/sql-server-management-studio/lesson-3-2-create-custom-templates.md)  
  
  
  

