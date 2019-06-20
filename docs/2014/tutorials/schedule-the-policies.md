---
title: Agendar as políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8becd7ad30acf1ea2a63feae4760091aede70c06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033498"
---
# <a name="schedule-the-policies"></a>Agendar as políticas
  Nesta tarefa, você agendará as políticas de práticas recomendadas que você importou na tarefa anterior.  
  
### <a name="to-schedule-the-best-practices-policies"></a>Para agendar as políticas de práticas recomendadas  
  
1.  No Pesquisador de objetos, expanda **Management**, expanda **gerenciamento de política**, expanda **políticas**, uma política de práticas recomendadas com o botão direito e, em seguida, clique em  **Propriedades**.  
  
    > [!NOTE]  
    >  Como alternativa, para ver facilmente quais políticas estão associadas com as práticas recomendadas para classificar os melhores práticas e categorias, expanda **Management**, expanda **gerenciamento de política**e, em seguida, clique em **Diretivas**. No menu **Exibir** , clique em **Detalhes do Pesquisador de Objetos**. No **detalhes do Pesquisador** painel, clique no **categoria** título para classificar as diretivas por categoria. As políticas de práticas recomendadas têm o prefixo **práticas recomendadas da Microsoft**. A política que você deseja configurar e, em seguida, clique com o botão direito **propriedades**.  
  
2.  No **gerais** página do **abrir política** na caixa a **modo de avaliação** , clique em **em agendamento**.  
  
3.  Ao lado de **agenda** , clique em **escolher** para especificar uma agenda existente ou clique em **New** para criar uma nova agenda.  
  
4.  Depois de configurar uma agenda, você pode selecionar o **Enabled** caixa de seleção próxima à parte superior da página para habilitar a política agendada.  
  
5.  Repita as etapas de 1 a 4 para cada política que você deseja agendar.  
  
    > [!NOTE]  
    >  Para exibir os resultados da avaliação após a execução de uma diretiva agendada, abra o log Histórico da Diretiva na instância de destino. Para abrir o log, clique com botão direito **gerenciamento de política**e, em seguida, clique em **Exibir histórico**.  
  
## <a name="summary"></a>Resumo  
 Você configurou políticas agendadas para serem executadas em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se você desejar implantar políticas agendadas em várias instâncias, continue na próxima tarefa deste tutorial.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Implantar diretivas agendadas em várias instâncias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
