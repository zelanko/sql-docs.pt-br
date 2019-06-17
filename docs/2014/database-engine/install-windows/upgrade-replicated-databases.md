---
title: Fazer upgrade de bancos de dados replicados | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a356a6bad7b0756f148b43ed0cbf35e8d2ce9cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775310"
---
# <a name="upgrade-replicated-databases"></a>Atualizar bancos de dados replicados
  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] suporta a atualização de bancos de dados replicados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; não é necessário interromper a atividade de outros nós durante a atualização de um nó. Verifique se você está em conformidade com as regras que dizem respeito às versões suportadas em uma topologia:  
  
-   Um Distribuidor pode ser de qualquer versão, desde que ela seja maior ou igual à do Publicador (em muitos casos, o Distribuidor tem a mesma instância que o Publicador).  
  
-   Um Publicador pode ser de qualquer versão, contanto que ela seja menor ou igual à versão do Distribuidor.  
  
-   A versão de assinante depende do tipo de publicação:  
  
    -   Um Assinante de uma publicação transacional pode ser de qualquer uma das duas versões do Publicador. Por exemplo, um Publicador do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] pode ter Assinantes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e um Publicador do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pode ter Assinantes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
    -   Um Assinante de uma publicação de mesclagem pode ser de qualquer versão menor ou igual à do Publicador.  
  
> [!NOTE]  
>  Esse tópico está disponível na documentação de Ajuda da instalação e nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os links do tópico que aparecem em negrito na documentação da Ajuda da instalação se referem a tópicos que só estão disponíveis nos Manuais Online.  
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>Executar o Log Reader Agent para replicação transacional antes da atualização  
 Antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você deve verificar se todas as transações confirmadas de tabelas publicadas foram processadas pelo Log Reader Agent. Para isso, execute as seguintes etapas para cada banco de dados que contém publicações transacionais:  
  
1.  Verifique se o Log Reader Agent está executando para o banco de dados. Por padrão, o agente é executado continuamente.  
  
2.  Interrompa a atividade de usuário em tabelas publicadas.  
  
3.  Conceda um tempo para que o Log Reader Agent copie transações para o banco de dados de distribuição e, depois, interrompa o agente.  
  
4.  Execute [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) para verificar se todas as transações foram processadas. O conjunto de resultados deste procedimento deve ser vazio.  
  
5.  Execute [sp_replflush](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql) para fechar a conexão de sp_replcmds.  
  
6.  Execute a atualização do servidor para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
7.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e o Log Reader Agent se eles não iniciarem automaticamente depois da atualização.  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>Executar agentes para replicação de mesclagem após a atualização  
 Depois da atualização, execute o Snapshot Agent para cada publicação de mesclagem e o Merge Agent para cada assinatura a fim de atualizar os metadados de replicação. Você não precisa aplicar o novo instantâneo, pois não é necessário reinicializar assinaturas. Metadados de assinatura são atualizados a primeira vez que o Merge Agent é executado após a atualização. Isso significa que o banco de dados de assinatura pode permanecer online e ativo durante a atualização do Publicador.  
  
 A replicação de mesclagem armazena metadados de publicação e de assinatura em várias tabelas do sistema nos bancos de dados de publicação e de assinatura. Executar o Snapshot Agent atualiza os metadados de publicação, e executar o Merge Agent atualiza os metadados de assinatura. Só é necessário gerar um instantâneo de publicação. Se uma publicação de mesclagem usar filtros com parâmetros, cada partição também terá um instantâneo. Não é necessário atualizar esses instantâneos particionados.  
  
 Execute os agentes do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Replication Monitor ou da linha de comando. Para obter mais informações sobre como executar o Snapshot Agent, consulte os seguintes tópicos:  
  
-   [Criar e aplicar o instantâneo inicial](../../../2014/relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Iniciar e interromper um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   [Criar e aplicar o instantâneo inicial](../../../2014/relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Conceitos dos executáveis do Replication Agent](../../../2014/relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
 Para obter mais informações sobre como executar o Merge Agent, consulte os seguintes tópicos:  
  
-   [Sincronizar uma assinatura pull](../../../2014/relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar uma assinatura push](../../../2014/relational-databases/replication/synchronize-a-push-subscription.md)  
  
 Depois de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma topologia que utiliza a replicação de mesclagem, altere o nível de compatibilidade de publicação de qualquer publicação caso queira usar novos recursos.  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>Atualizando as edições Standard, Workgroup ou Express  
 Antes de fazer upgrade de uma edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para outra, verifique se há suporte para a funcionalidade atualmente utilizada na edição para a qual deseja fazer upgrade. Para obter mais informações, consulte a seção sobre replicação em [recursos compatíveis com as edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="web-synchronization-for-merge-replication"></a>Sincronização da Web para replicação de mesclagem.  
 A opção de sincronização da Web para replicação de mesclagem requer que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) seja copiado para o diretório virtual do servidor IIS (Serviços de Informações da Internet) usado para sincronização. Quando você configura a sincronização da Web, o arquivo é copiado para o diretório virtual pelo Assistente para Configuração da Sincronização da Web. Se você atualizar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no servidor IIS, deverá copiar replisapi.dll manualmente do diretório COM para o diretório virtual no servidor IIS. Para obter mais informações sobre como configurar a sincronização da Web, veja [Configurar sincronização da Web](../../../2014/relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>Restaurando um banco de dados replicado de uma versão anterior  
 Para assegurar que as configurações de replicação sejam mantidas na restauração do backup de um banco de dados replicado de uma versão anterior, restaure para um servidor e um banco de dados que tenham os mesmos nomes que o servidor e o banco de dados dos quais foi obtido o backup.  
  
## <a name="see-also"></a>Consulte também  
 [Perguntas Frequentes sobre Administração de Replicação](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Compatibilidade com versões anteriores de replicação](../../../2014/relational-databases/replication/replication-backward-compatibility.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)  
  
  
