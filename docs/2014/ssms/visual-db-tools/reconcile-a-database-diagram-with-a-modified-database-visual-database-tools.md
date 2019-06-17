---
title: Reconciliar um diagrama de banco de dados com um banco de dados modificado (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d779e6362cc3e2842003b82a092ce48ce4933e8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011379"
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>Reconciliar um diagrama de banco de dados com um banco de dados modificado (Visual Database Tools)
  Você salva seu diagrama de banco de dados, quando estiver pronto para atualizar o banco de dados, de forma que ele corresponda ao seu diagrama. Porém, se outros usuários tiverem atualizado o banco de dados desde que você abriu seu diagrama, essas alterações podem afetar seu diagrama e vice-versa.  
  
 Salvar seu diagrama reconciliará o banco de dados com seu diagrama, substituindo as alterações de outros usuários para que o banco de dados corresponda ao seu diagrama.  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>Para atualizar um banco de dados para que ele corresponda ao seu diagrama  
  
1.  Salve seu diagrama de banco de dados  
  
     Se você não salvou seu diagrama anteriormente, digite um nome para o diagrama na caixa de diálogo **Salvar Novo Diagrama de Banco de Dados** e escolha **OK**.  
  
2.  A caixa de diálogo **Salvar** lista as tabelas que serão afetadas quando você salvar seu diagrama. Escolha **Sim** para continuar.  
  
3.  A caixa de diálogo **Alterações de Banco de Dados Detectadas** lista os objetos que foram modificados e serão alterados para corresponder a seu diagrama. Escolha **Sim** para salvar o diagrama e aceitar a lista de alterações.  
  
    > [!NOTE]  
    >  Se seu diagrama contiver tabelas e colunas que foram excluídas no banco de dados, só suas definições serão recriadas no banco de dados quando você salvar seu diagrama. Este processo não restaura quaisquer dados que existiam nestes objetos antes de sua exclusão.  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>Para atualizar seu diagrama para que ele corresponda a um banco de dados modificado  
  
1.  Feche seu diagrama sem salvar as alterações.  
  
2.  Clique com o botão direito no diagrama no Pesquisador de Objetos  
  
3.  No menu de atalho, clique em **Atualizar**.  
  
4.  Reabra o diagrama.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
