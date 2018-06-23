---
title: Agendar as políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 99c6e3a4eacfea76ff16ea266d38f2087c088f33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010801"
---
# <a name="schedule-the-policies"></a>Agendar as políticas
  Nesta tarefa, você agendará as políticas de práticas recomendadas que você importou na tarefa anterior.  
  
### <a name="to-schedule-the-best-practices-policies"></a>Para agendar as políticas de práticas recomendadas  
  
1.  No Pesquisador de objetos, expanda **gerenciamento**, expanda **gerenciamento de política de**, expanda **políticas**, clique com botão direito uma política de práticas recomendadas e, em seguida, clique em  **Propriedades**.  
  
    > [!NOTE]  
    >  Como alternativa, para ver facilmente quais políticas estão associadas com as práticas recomendadas para classificar as melhores práticas e categorias, expanda **gerenciamento**, expanda **gerenciamento de política de**e, em seguida, clique em **Políticas**. No menu **Exibir** , clique em **Detalhes do Pesquisador de Objetos**. No **detalhes do Pesquisador** painel, clique no **categoria** título para classificar as diretivas por categoria. As políticas de práticas recomendadas têm o prefixo **práticas recomendadas da Microsoft**. Com o botão direito na diretiva que você deseja configurar e, em seguida, clique em **propriedades**.  
  
2.  No **geral** página do **abrir política** na caixa de **modo de avaliação** lista, clique em **na agenda**.  
  
3.  Ao lado de **agenda** , clique em **escolher** para especificar uma agenda existente ou clique em **novo** para criar uma nova agenda.  
  
4.  Depois de configurar uma agenda, você pode selecionar o **habilitado** caixa de seleção na parte superior da página para habilitar a política agendada.  
  
5.  Repita as etapas de 1 a 4 para cada política que você deseja agendar.  
  
    > [!NOTE]  
    >  Para exibir os resultados da avaliação após a execução de uma diretiva agendada, abra o log Histórico da Diretiva na instância de destino. Para abrir o log, clique com botão direito **gerenciamento de política de**e, em seguida, clique em **Exibir histórico**.  
  
## <a name="summary"></a>Resumo  
 Você configurou políticas agendadas para serem executadas em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se você desejar implantar políticas agendadas em várias instâncias, continue na próxima tarefa deste tutorial.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Implantar diretivas agendadas em várias instâncias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  