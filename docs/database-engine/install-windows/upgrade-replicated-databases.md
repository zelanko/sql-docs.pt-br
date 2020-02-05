---
title: Atualizar ou aplicar patch a bancos de dados replicados | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2016
ms.prod: sql
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 46156a9e7b1180d5ed70f0dbcb6b25d2f608f0fc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72008460"
---
# <a name="upgrade-or-patch-replicated-databases"></a>Atualizar ou aplicar patches a bancos de dados replicados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  O [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] suporta a atualização de bancos de dados replicados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; não é necessário interromper a atividade de outros nós durante a atualização de um nó. Verifique se você está em conformidade com as regras que dizem respeito às versões suportadas em uma topologia:  
  
-   Um Distribuidor pode ser de qualquer versão, desde que ela seja maior ou igual à do Publicador (em muitos casos, o Distribuidor tem a mesma instância que o Publicador).    
-   Um Publicador pode ser de qualquer versão, contanto que ela seja menor ou igual à versão do Distribuidor.    
-   A versão de assinante depende do tipo de publicação:    
    - Um Assinante de uma publicação transacional pode ser de qualquer uma das duas versões do Publicador. Por exemplo: um publicador do SQL Server 2012 (11.x) pode ter assinantes do SQL Server 2014 (12.x) e SQL Server 2016 (13.x); e um publicador do SQL Server 2016 (13.x) pode ter assinantes do SQL Server 2014 (12.x) e SQL Server 2012 (11.x).     
    - Um assinante de uma publicação de mesclagem pode ser todas as versões iguais ou anteriores à versão do publicador com suporte, de acordo com o ciclo de vida de suporte das versões.  
 
O caminho de atualização para o SQL Server é diferente dependendo do padrão de implantação. O SQL Server oferece dois caminhos de atualização em geral:
- Lado a lado: implantar um ambiente paralelo e mover bancos de dados juntamente com os objetos de nível de instância associada, como logons, trabalhos, etc. para o novo ambiente. 
- Atualização in-loco: permitir que a mídia de instalação do SQL Server atualize a instalação do SQL Server existente, substituindo os bits do SQL Server e atualizando os objetos de banco de dados. Para ambientes que executam Grupos de Disponibilidade AlwaysOn ou Instâncias do Cluster de Failover, uma atualização in-loco é combinada com uma [atualização sem interrupção](choose-a-database-engine-upgrade-method.md#rolling-upgrade) para minimizar o tempo de inatividade. 

Uma abordagem comum que tem sido adotada para atualizações lado a lado de topologias de replicação é mover os pares publicador-assinante em partes para o novo ambiente lado a lado em vez de uma movimentação de toda a topologia. Essa abordagem em fases ajuda a controlar o tempo de inatividade e a minimizar o impacto a uma determinada medida para o negócio dependente de replicação.  

A maior parte deste artigo está no escopo para atualizar a versão do SQL Server. No entanto, o processo de atualização in-loco também deve ser usado ao aplicar um patch ao SQL Server com um service pack ou atualização cumulativa também. 

 >[!WARNING]
 > A atualização de uma topologia de replicação é um processo de várias etapas. Recomendamos tentar uma atualização de uma réplica de sua topologia de replicação em um ambiente de teste antes de executar a atualização no ambiente de produção real. Isso ajudará a corrigir qualquer documentação operacional necessária para lidar com a atualização facilmente sem incorrer em tempos de inatividade caros e longos durante o processo de atualização real. Vimos clientes reduzirem o tempo de inatividade significativamente com o uso dos Grupos de Disponibilidade Always On e/ou Instâncias do Cluster de Failover do SQL Server para seus ambientes de produção ao atualizar sua topologia de replicação. Além disso, recomendamos fazer backups de todos os bancos de dados, incluindo MSDB, bancos de dados Mestre, de Distribuição e os bancos de dados do usuário que participam da replicação antes de tentar a atualização.


## <a name="replication-matrix"></a>Matriz de replicação

[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>Executar o Log Reader Agent para replicação transacional antes da atualização  
 Antes de fazer upgrade para o [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)], você deve verificar se todas as transações confirmadas das tabelas publicadas foram processadas pelo Agente de Leitor de Log. Para isso, execute as seguintes etapas para cada banco de dados que contém publicações transacionais:  
  
1.  Verifique se o Log Reader Agent está executando para o banco de dados. Por padrão, o agente é executado continuamente.    
2.  Interrompa a atividade de usuário em tabelas publicadas.  
3.  Conceda um tempo para que o Log Reader Agent copie transações para o banco de dados de distribuição e, depois, interrompa o agente.  
4.  Execute [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) para verificar se todas as transações foram processadas. O conjunto de resultados deste procedimento deve ser vazio.   
5.  Execute [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) para fechar a conexão de sp_replcmds.   
6.  Execute a atualização do servidor para a última versão do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].   
7.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e o Log Reader Agent se eles não iniciarem automaticamente depois da atualização.  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>Executar agentes para replicação de mesclagem após a atualização  
 Depois da atualização, execute o Snapshot Agent para cada publicação de mesclagem e o Merge Agent para cada assinatura a fim de atualizar os metadados de replicação. Você não precisa aplicar o novo instantâneo, pois não é necessário reinicializar assinaturas. Metadados de assinatura são atualizados a primeira vez que o Merge Agent é executado após a atualização. Isso significa que o banco de dados de assinatura pode permanecer online e ativo durante a atualização do Publicador.  
  
 A replicação de mesclagem armazena metadados de publicação e de assinatura em várias tabelas do sistema nos bancos de dados de publicação e de assinatura. Executar o Snapshot Agent atualiza os metadados de publicação, e executar o Merge Agent atualiza os metadados de assinatura. Só é necessário gerar um instantâneo de publicação. Se uma publicação de mesclagem usar filtros com parâmetros, cada partição também terá um instantâneo. Não é necessário atualizar esses instantâneos particionados.  
  
 Execute os agentes do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Replication Monitor ou da linha de comando. Para obter mais informações sobre como executar o Agente de Instantâneo, consulte os seguintes artigos:  
  
-   [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [Iniciar e interromper um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)
-   [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [Conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  

Para obter mais informações sobre como executar o Agente de Mesclagem, consulte os seguintes artigos:
-   [Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)
-   [Sincronizar uma assinatura push](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  

Depois de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma topologia que utiliza a replicação de mesclagem, altere o nível de compatibilidade de publicação de qualquer publicação caso queira usar novos recursos.  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>Atualizando as edições Standard, Workgroup ou Express  
Antes de fazer upgrade de uma edição do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] para outra, verifique se há suporte para a funcionalidade atualmente utilizada na edição para a qual deseja fazer upgrade. Para obter mais informações, consulte a seção sobre Replicação em [Edições e recursos com suporte do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md).  

## <a name="steps-to-upgrade-a-replication-topology"></a>Etapas para atualizar uma topologia de replicação
Essas etapas descrevem a ordem na qual os servidores em uma topologia de replicação devem ser atualizados. As mesmas etapas serão aplicáveis se você estiver executando uma replicação transacional ou de mesclagem. No entanto, essas etapas não abrangem a replicação Ponto a Ponto, assinaturas de atualização enfileiradas nem assinaturas de atualização imediatas. 

### <a name="in-place-upgrade"></a>Atualização in-loco 
1. Atualize o distribuidor. 
2. Atualize o publicador e o assinante. Eles podem ser atualizados em qualquer ordem. 

 >[!NOTE]
 > Para o SQL 2008 e 2008 R2, a atualização do publicador e do assinante deve ser feita ao mesmo tempo para alinhar-se à matriz de topologia de replicação. Um publicador ou assinante do SQL 2008 ou 2008R2 não pode ter um publicador nem um assinante do SQL 2016 (ou superior). Se não for possível atualizar ao mesmo tempo, use uma atualização intermediária para atualizar as instâncias do SQL para SQL 2014 e, em seguida, atualize-as novamente para o SQL 2016 (ou superior).  

### <a name="side-by-side-upgrade"></a>Atualização lado a lado
1. Atualize o distribuidor.
1. Reconfigure a [distribuição](../../relational-databases/replication/configure-distribution.md) na nova instância do SQL Server.
1. Atualize o publicador.
1. Atualize o assinante.
1. Reconfigure todos os pares publicador-assinante, incluindo a reinicialização do assinante. 


## <a name="steps-for-side-by-side-migration-of-the-distributor-to-windows-server-2012-r2"></a>Etapas para a migração lado a lado do distribuidor para o Windows Server 2012 R2
Se estiver planejando atualizar a instância do SQL Server para o SQL Server 2016 (ou superior) e seu sistema operacional atual for o Windows 2008 (ou 2008 R2), será necessário realizar uma atualização lado a lado do sistema operacional para o Windows Server R2 ou superior. O motivo dessa atualização intermediária do sistema operacional é que o SQL Server 2016 não pode ser instalado em um Windows Server 2008/2008 R2 e o Windows Server 2008/20008 R2 não permite atualizações in-loco diretamente para Windows Server 2016. Embora seja possível executar uma atualização in-loco do Windows Server 2008/2008 R2 para o Windows Server 2012 e, em seguida, para o Windows Server 2016, isso geralmente não é recomendado devido ao tempo de inatividade e à complexidade adicional, impedindo um caminho de reversão fácil. Um upgrade lado a lado é o único caminho de atualização disponível para instâncias do SQL Server que participam de um cluster de failover.  As etapas a seguir podem ser executadas de uma instância autônoma do SQL Server ou em uma dentro de uma FCI (Instância do Cluster de Failover) Always On.

1. Configure uma nova instância do SQL Server (autônoma ou Cluster de Failover Always On), uma edição e uma versão como seu distribuidor no Windows Server 2012 R2/2016 com um cluster do Windows diferente um nome do FCI do SQL Server ou nome do host autônomo. Será necessário manter a mesma estrutura de diretório que a do distribuidor antigo para garantir que os executáveis dos agentes de replicação, pastas de replicação e caminhos do arquivo de banco de dados sejam encontrados no mesmo caminho no novo ambiente. Isso reduzirá quaisquer etapas de pós-migração/atualização necessárias.
1. Certifique-se de que sua replicação está sincronizada e, em seguida, desligue todos os agentes de replicação. 
1. Desligue a instância atual do Distribuidor do SQL Server. Se for uma instância autônoma, desligue o servidor. Se for um FCI do SQL, coloque toda a função do SQL Server offline no gerenciador de cluster, incluindo o nome da rede. 
1. Remova a DNS e as entradas do objeto de computador do AD do ambiente antigo (instância de distribuidor atual). 
1. Altere o nome do host do novo servidor para coincidir com o do servidor antigo.
    1. Se for um FCI do SQL, renomeie o novo FCI do SQL com o mesmo nome do servidor virtual que o da instância antiga. 
1. Copie os arquivos de banco de dados da instância anterior usando o redirecionamento SAN, cópia de armazenamento ou cópia de arquivo. 
1. Coloque a nova instância do SQL Server online. 
1. Reinicie todos os agentes de replicação e verifique se eles estão sendo executados com êxito.
1. Valide se a replicação está funcionando conforme esperado. 
1. Use a mídia de instalação do SQL Server para executar uma atualização in-loco de sua instância do SQL Server para a nova versão do SQL Server. 


  >[!NOTE]
  > Para reduzir o tempo de inatividade, recomendamos que você execute a *migração lado a lado* do distribuidor como uma atividade e a *atualização in-loco no SQL Server 2016* como outra atividade. Isso permitirá que você adote uma abordagem em fases, reduza o risco e minimize o tempo de inatividade.

## <a name="web-synchronization-for-merge-replication"></a>Sincronização da Web para replicação de mesclagem.  
 A opção de sincronização da Web para replicação de mesclagem requer que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) seja copiado para o diretório virtual do servidor IIS (Serviços de Informações da Internet) usado para sincronização. Quando você configura a sincronização da Web, o arquivo é copiado para o diretório virtual pelo Assistente para Configuração da Sincronização da Web. Se você atualizar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no servidor IIS, deverá copiar replisapi.dll manualmente do diretório COM para o diretório virtual no servidor IIS. Para obter mais informações sobre como configurar a sincronização da Web, veja [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>Restaurando um banco de dados replicado de uma versão anterior  
 Para assegurar que as configurações de replicação sejam mantidas na restauração do backup de um banco de dados replicado de uma versão anterior, restaure para um servidor e um banco de dados que tenham os mesmos nomes que o servidor e o banco de dados dos quais foi obtido o backup.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação do SQL Server](../../relational-databases/replication/sql-server-replication.md)  
 [Perguntas Frequentes sobre Administração de Replicação](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Compatibilidade com versões anteriores de replicação](../../relational-databases/replication/replication-backward-compatibility.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 [Atualizando uma topologia de replicação para o SQL Server 2016](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/)
