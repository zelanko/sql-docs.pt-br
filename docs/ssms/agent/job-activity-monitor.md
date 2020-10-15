---
description: Monitor de Atividade do Trabalho
title: Monitor de Atividade do Trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.jobactivitymonitor.alljobs.f1
- SQL13.SWB.ACTIVITYMON.F1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 813740790db9a7f9bb15f8e5d2a003b73ba5a88f
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037939"
---
# <a name="job-activity-monitor"></a>Monitor de Atividade do Trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Use esta página para exibir a atividade atual de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Clique em **Filtrar** para limitar os trabalhos exibidos. A grade **Atividade do Trabalho do Agent** é somente leitura. Clique nos cabeçalhos das coluna para classificar a grade. Para modificar um trabalho, clique duas vezes no trabalho para abrir a caixa de diálogo **Propriedades do Trabalho** . Clique com o botão direito do mouse em um trabalho na grade para que ele inicie a execução de todas as etapas do trabalho, inicie em uma etapa de trabalho específica, desabilite ou habilite o trabalho, atualize o trabalho, exclua o trabalho, exiba o histórico do trabalho ou exiba suas propriedades. Clique em **Atualizar** , para atualizar a grade com informações atuais.  
  
## <a name="options"></a>Opções  
**Nome**  
Nome do trabalho.  
  
**Enabled**  
Se o trabalho está habilitado (**sim**) ou desabilitado (**não**).  
  
**Status***  
Status atual do trabalho.  
  
**Resultado da Última Execução**  
Status do trabalho quando executado pela última vez.  
  
**Última Execução**  
Data e hora em que o trabalho foi executado pela última vez, usando a data e hora locais do servidor.  
  
**Próxima Execução***  
Date e hora em que o trabalho está agendado para ser executado usando a data local e hora locais do servidor.  
  
**Categoria**  
A categoria de trabalho atribuída ao trabalho.  
  
**Executável**  
**Sim** se o trabalho puder ser executado; **Não** se o trabalho não puder ser executado. Um trabalho não é executável se não tiver nenhuma etapa ou se não tiver nenhum servidor de destino.  
  
**Agendado**  
**Sim** se o trabalho estiver atribuído a uma agenda de trabalho; **Não** se o trabalho não tiver nenhuma agenda.  
  
*Apenas membros da função de servidor fixa sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do grupo de administradores do servidor podem ver os valores dessa coluna. Os membros da função SQLAgentOperatorRole não podem ver os valores dessa coluna.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Para abrir o Monitor de Atividade do Trabalho  
  
-   No **Pesquisador de Objetos**, expanda seu servidor, expanda **SQL Server Agent**, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
## <a name="see-also"></a>Consulte Também  
[Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
