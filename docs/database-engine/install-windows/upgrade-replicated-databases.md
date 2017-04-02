---
title: "Atualizar bancos de dados replicados | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atualizações de bancos de dados de replicação de mesclagem [replicação do SQL Server]"
  - "replicação [SQL Server], atualizando"
  - "replicação transacional, atualizando bancos de dados"
  - "replicação de instantâneo [SQL Server], atualizando bancos de dados"
  - "atualizando bancos de dados replicados"
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
caps.latest.revision: 74
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 73
---
# Atualizar bancos de dados replicados
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] suporta a atualização de bancos de dados replicados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; não é necessário interromper a atividade de outros nós durante a atualização de um nó. Verifique se você está em conformidade com as regras que dizem respeito às versões suportadas em uma topologia:  
  
-   Um Distribuidor pode ser de qualquer versão, desde que ela seja maior ou igual à do Publicador (em muitos casos, o Distribuidor tem a mesma instância que o Publicador).  
  
-   Um Publicador pode ser de qualquer versão, contanto que ela seja menor ou igual à versão do Distribuidor.  
  
-   A versão de assinante depende do tipo de publicação:  
  
    -   Um Assinante de uma publicação transacional pode ser de qualquer uma das duas versões do Publicador. Por exemplo: um Publicador do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] pode ter Assinantes do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ; e um Editor do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] pode ter Assinantes do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e do  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
    -   Um Assinante de uma publicação de mesclagem pode ser de qualquer versão menor ou igual à do Publicador.  
  
> [!NOTE]  
>  Esse tópico está disponível na documentação de Ajuda da instalação e nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os links do tópico que aparecem em negrito na documentação da Ajuda da instalação se referem a tópicos que só estão disponíveis nos Manuais Online.  
  
## Executar o Log Reader Agent para replicação transacional antes da atualização  
 Antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você deve verificar se todas as transações confirmadas de tabelas publicadas foram processadas pelo Log Reader Agent. Para isso, execute as seguintes etapas para cada banco de dados que contém publicações transacionais:  
  
1.  Verifique se o Log Reader Agent está executando para o banco de dados. Por padrão, o agente é executado continuamente.  
  
2.  Interrompa a atividade de usuário em tabelas publicadas.  
  
3.  Conceda um tempo para que o Log Reader Agent copie transações para o banco de dados de distribuição e, depois, interrompa o agente.  
  
4.  Execute [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) para verificar se todas as transações foram processadas. O conjunto de resultados deste procedimento deve ser vazio.  
  
5.  Execute [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) para fechar a conexão de sp_replcmds.  
  
6.  Execute a atualização do servidor para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
7.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e o Log Reader Agent se eles não iniciarem automaticamente depois da atualização.  
  
## Executar agentes para replicação de mesclagem após a atualização  
 Depois da atualização, execute o Snapshot Agent para cada publicação de mesclagem e o Merge Agent para cada assinatura a fim de atualizar os metadados de replicação. Você não precisa aplicar o novo instantâneo, pois não é necessário reinicializar assinaturas. Metadados de assinatura são atualizados a primeira vez que o Merge Agent é executado após a atualização. Isso significa que o banco de dados de assinatura pode permanecer online e ativo durante a atualização do Publicador.  
  
 A replicação de mesclagem armazena metadados de publicação e de assinatura em várias tabelas do sistema nos bancos de dados de publicação e de assinatura. Executar o Snapshot Agent atualiza os metadados de publicação, e executar o Merge Agent atualiza os metadados de assinatura. Só é necessário gerar um instantâneo de publicação. Se uma publicação de mesclagem usar filtros com parâmetros, cada partição também terá um instantâneo. Não é necessário atualizar esses instantâneos particionados.  
  
 Execute os agentes do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Replication Monitor ou da linha de comando. Para obter mais informações sobre como executar o Snapshot Agent, consulte os seguintes tópicos:  
  
-   [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Iniciar e interromper um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
 Para obter mais informações sobre como executar o Merge Agent, consulte os seguintes tópicos:  
  
-   [Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar uma assinatura push](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
 Depois de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma topologia que utiliza a replicação de mesclagem, altere o nível de compatibilidade de publicação de qualquer publicação caso queira usar novos recursos.  
  
## Atualizando as edições Standard, Workgroup ou Express  
 Antes de atualizar de uma edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para outra, verifique se a funcionalidade que você está usando tem suporte na edição para a qual deseja atualizar. Para obter mais informações, veja a seção sobre Replicação em [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## Sincronização da Web para replicação de mesclagem.  
 A opção de sincronização da Web para replicação de mesclagem requer que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) seja copiado para o diretório virtual do servidor IIS (Serviços de Informações da Internet) usado para sincronização. Quando você configura a sincronização da Web, o arquivo é copiado para o diretório virtual pelo Assistente para Configuração da Sincronização da Web. Se você atualizar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no servidor IIS, deverá copiar replisapi.dll manualmente do diretório COM para o diretório virtual no servidor IIS. Para obter mais informações sobre como configurar a sincronização da Web, veja [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Restaurando um banco de dados replicado de uma versão anterior  
 Para assegurar que as configurações de replicação sejam mantidas na restauração do backup de um banco de dados replicado de uma versão anterior, restaure para um servidor e um banco de dados que tenham os mesmos nomes que o servidor e o banco de dados dos quais foi obtido o backup.  
  
## Consulte também  
 [Administração &#40;Replicação&#41;](../../relational-databases/replication/administration/administration-replication.md)   
 [Compatibilidade com versões anteriores de replicação](../../relational-databases/replication/replication-backward-compatibility.md)   
 [Novidades &#40;Replicação&#41;](../../relational-databases/replication/what-s-new-replication.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Atualizar para o SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
  
  