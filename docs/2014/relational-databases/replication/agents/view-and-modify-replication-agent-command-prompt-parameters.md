---
title: Exibir e modificar parâmetros do prompt de comando do agente de replicação (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e4327de10dd03b3ff8cf034ade64391d18d2a86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192892"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters-sql-server-management-studio"></a>Exibir e modificar parâmetros do prompt de comando de agentes de replicação (SQL Server Management Studio)
  Agentes de replicação são executáveis que aceitam parâmetros de linha de comando. Por padrão, os agentes são executados nas etapas de trabalho do Agent [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, portanto, esses parâmetros podem ser exibidos e modificados usando a caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** . Essa caixa de diálogo está disponível na pasta **Trabalhos** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e na guia **Agentes** no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
> [!NOTE]  
>  As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente.  
  
 Embora seja possível modificar os parâmetros diretamente, em geral, eles são modificados através de um perfil de agente. Para saber mais, confira [Replication Agent Profiles](replication-agent-profiles.md).  
  
 Ao acessar os trabalhos de agentes na pasta **Trabalhos** use a tabela a seguir, para determinar o nome do trabalho do agente e os parâmetros disponíveis para cada agente.  
  
|Agente|Nome do trabalho|Para uma lista de parâmetros, confira...|  
|-----------|--------------|------------------------------------|  
|Snapshot Agent|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Snapshot Agent para uma partição de publicação de mesclagem|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Agente de Leitor de Log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|[Agente do Leitor de Log de Replicação](replication-log-reader-agent.md)|  
|Merge Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Merge Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Distribution Agent para assinaturas push|**\<\<\<Publicador>-PublicationDatabase>-publicação>-Subscriber>\<-inteiro>1 \<** <sup></sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Distribution Agent para assinaturas pull|**\<\<\<\<Publicador>-PublicationDatabase>-publicação>-Subscriber>-SubscriptionDatabase>\<-GUID>2 \<** <sup></sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Queue Reader Agent|**[\<Distributor>].\<integer>**|[Agente de Leitor de Fila de Replicação](replication-queue-reader-agent.md)|  
  
 <sup>1</sup> para assinaturas push para publicações Oracle, é ** \<Publicador>-\<Publisher**> em vez de ** \<Publisher>\<-PublicationDatabase>**  
  
 <sup>2</sup> para assinaturas pull para publicações Oracle, é ** \<Publicador>\<-DistributionDatabase**> em vez de ** \<Publicador>-\<PublicationDatabase>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Para exibir e modificar os parâmetros da linha de comando dos agentes de replicação do Management Studio  
  
1.  Conecte-se ao computador adequado em [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], e expanda o servidor.  
  
    -   Para assinatura pull no Agente de Distribuição e no Agente de Mesclagem, conecte-se com o Assinante.  
  
    -   Para todos os demais agentes, conecte-se com o Distribuidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse em um trabalho e clique em **Propriedades**.  
  
4.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
5.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Para exibir e modificar os parâmetros da linha de comando do Agente de Distribuição e do Agente de Mesclagem do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse em uma assinatura e clique em **Exibir Detalhes**.  
  
4.  Na janela **assinatura \< assinatura>** , clique em **ação**e, em seguida, clique em ** \<AgentName> Propriedades do trabalho**.  
  
5.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
6.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
7.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Para exibir e modificar parâmetros de linha de comando do Replication Monitor do Agente de Instantâneo, do Agente de Leitor de Log e do Agente de Leitor de Fila.  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique com o botão direito do mouse em um agente na grade e em **Propriedades**.  
  
4.  Na página **Etapas** da caixa de diálogo **Propriedades do Trabalho – \<Trabalho>** , selecione a etapa **Executar agente** e clique em **Editar**.  
  
5.  Na caixa de diálogo **Propriedades da Etapa do Trabalho – Executar agente** , edite o campo **Comando** .  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](replication-agent-administration.md)   
 [Conceitos dos executáveis do Agente de Replicação](../concepts/replication-agent-executables-concepts.md)   
 [Visão geral dos agentes de replicação](replication-agents-overview.md)  
  
  
