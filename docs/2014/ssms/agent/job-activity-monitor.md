---
title: Monitor de Atividade do Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.ACTIVITYMON.F1
- sql12.ag.jobactivitymonitor.alljobs.f1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 58f04e83541f218a4cdcfbd99d6b3de12bf38b2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064975"
---
# <a name="job-activity-monitor"></a>Monitor de Atividade do Trabalho
  Use esta página para exibir a atividade atual de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Clique em **Filtrar** para limitar os trabalhos exibidos. A grade **Atividade do Trabalho do Agent** é somente leitura. Clique nos cabeçalhos das coluna para classificar a grade. Para modificar um trabalho, clique duas vezes no trabalho para abrir a caixa de diálogo **Propriedades do Trabalho** . Clique com o botão direito do mouse em um trabalho na grade para que ele inicie a execução de todas as etapas do trabalho, inicie em uma etapa de trabalho específica, desabilite ou habilite o trabalho, atualize o trabalho, exclua o trabalho, exiba o histórico do trabalho ou exiba suas propriedades. Clique em **Atualizar** , para atualizar a grade com informações atuais.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Nome do trabalho.  
  
 **Enabled**  
 Se o trabalho está habilitado (**sim**) ou desabilitado (**não**).  
  
 **Status** <sup>1</sup>  
 Status atual do trabalho.  
  
 **Resultado da Última Execução**  
 Status do trabalho quando executado pela última vez.  
  
 **Última Execução**  
 Data e hora em que o trabalho foi executado pela última vez, usando a data e hora locais do servidor.  
  
 **Próxima execução** <sup>1</sup>  
 Date e hora em que o trabalho está agendado para ser executado usando a data local e hora locais do servidor.  
  
 **Categoria**  
 A categoria de trabalho atribuída ao trabalho.  
  
 **Executável**  
 **Sim** se o trabalho puder ser executado; **Não** se o trabalho não puder ser executado. Um trabalho não é executável se não tiver nenhuma etapa ou se não tiver nenhum servidor de destino.  
  
 **Agendado**  
 **Sim** se o trabalho estiver atribuído a uma agenda de trabalho; **Não** se o trabalho não tiver nenhuma agenda.  
  
 <sup>1</sup> Somente os membros da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de servidor fixa sysadmin e do grupo de administradores de servidor podem ver os valores nesta coluna. Os membros da função SQLAgentOperatorRole não podem ver os valores dessa coluna.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Para abrir o Monitor de Atividade do Trabalho  
  
-   No **Pesquisador de Objetos**, expanda seu servidor, expanda **SQL Server Agent**, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar Atividade do Trabalho](monitor-job-activity.md)  
  
  
