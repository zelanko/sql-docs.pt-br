---
title: "Exibir e modificar par&#226;metros do prompt de comando de agentes de replica&#231;&#227;o (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agentes [replicação do SQL Server], parâmetros de prompt de comando"
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir e modificar par&#226;metros do prompt de comando de agentes de replica&#231;&#227;o (SQL Server Management Studio)
  Agentes de replicação são executáveis que aceitam parâmetros de linha de comando. Por padrão, os agentes executam sob [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] etapas de trabalho do Agent, para esses parâmetros podem ser exibidos e modificados usando o **Propriedades do trabalho - \< trabalho>** caixa de diálogo. Essa caixa de diálogo está disponível na pasta **Trabalhos** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e na guia **Agentes** no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  As alterações do parâmetro de agente entrarão em vigor na próxima vez o agente for iniciado. Se o agente ficar executando continuamente, será necessário parar e reiniciar o agente.  
  
 Embora seja possível modificar os parâmetros diretamente, em geral, eles são modificados através de um perfil de agente. Para obter mais informações, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Ao acessar os trabalhos de agentes na pasta **Trabalhos** use a tabela a seguir, para determinar o nome do trabalho do agente e os parâmetros disponíveis para cada agente.  
  
|Agente|Nome do trabalho|Para uma lista de parâmetros, consulte...|  
|-----------|--------------|------------------------------------|  
|Snapshot Agent|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< inteiro>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Snapshot Agent para uma partição de publicação de mesclagem|**Dyn_ \< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de Leitor de Log|**\< publicador>-\< Banco_de_dados_de_publicação>-\< inteiro>**|[Replication Agente de Leitor de Log](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Merge Agent para assinaturas pull|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< Banco_de_dados_de_assinatura>-\< inteiro>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Merge Agent para assinaturas push|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Distribution Agent para assinaturas push|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>***|[Agente de Distribuição de Replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Distribution Agent para assinaturas pull|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< Banco_de_dados_de_assinatura>-\< GUID>***\*|[Agente de Distribuição de Replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\< publicador>-\< Banco_de_dados_de_publicação>-\< publicação>-\< assinante>-\< inteiro>**|[Agente de Distribuição de Replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Queue Reader Agent|**[\< distribuidor>]. \< inteiro>**|[Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Para assinaturas push para publicações Oracle, é **\< publicador>-\< publicador**> em vez de **\< publicador>-\< banco De_dados_de_publicação>**  
  
 \*\*Para assinaturas pull para publicações Oracle, é **\< publicador>-\< Banco_de_dados_de_distribuição**> em vez de **\< publicador>-\< banco De_dados_de_publicação>**  
  
### Para exibir e modificar os parâmetros da linha de comando dos agentes de replicação do Management Studio  
  
1.  Conecte-se ao computador adequado em [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], e expanda o servidor.  
  
    -   Para assinatura pull no Agente de Distribuição e no Agente de Mesclagem, conecte-se com o Assinante.  
  
    -   Para todos os demais agentes, conecte-se com o Distribuidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Um trabalho de atalho e, em seguida, clique em **propriedades**.  
  
4.  No **etapas** página do **Propriedades do trabalho - \< trabalho>** caixa de diálogo, selecione a etapa **Executar Agente**, e, em seguida, clique em **Editar**.  
  
5.  No **Propriedades da etapa de trabalho - Run agent** caixa de diálogo, edite o **comando** campo.  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### Para exibir e modificar os parâmetros da linha de comando do Agente de Distribuição e do Agente de Mesclagem do Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique em uma assinatura e, em seguida, clique em **Exibir detalhes**.  
  
4.  No **assinatura \< Nome_da_assinatura >** janela, clique em **ação**, e, em seguida, clique em **\< Nome_do_agente> Propriedades do trabalho**.  
  
5.  No **etapas** página do **Propriedades do trabalho - \< trabalho>** caixa de diálogo, selecione a etapa **Executar Agente**, e, em seguida, clique em **Editar**.  
  
6.  No **Propriedades da etapa de trabalho - Run agent** caixa de diálogo, edite o **comando** campo.  
  
7.  Clique em **OK** , em ambas as caixas de diálogo.  
  
### Para exibir e modificar parâmetros de linha de comando do Replication Monitor do Agente de Instantâneo, do Agente de Leitor de Log e do Agente de Leitor de Fila.  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor, expanda um Publicador e, em seguida, clique em uma publicação.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique um agente na grade e, em seguida, clique em **propriedades**.  
  
4.  No **etapas** página do **Propriedades do trabalho - \< trabalho>** caixa de diálogo, selecione a etapa **Executar Agente**, e, em seguida, clique em **Editar**.  
  
5.  No **Propriedades da etapa de trabalho - Run agent** caixa de diálogo, edite o **comando** campo.  
  
6.  Clique em **OK** , em ambas as caixas de diálogo.  
  
## Consulte também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Visão geral dos agentes de replicação.](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  