---
title: "Estrat&#233;gias para fazer backup e restaurar a replica&#231;&#227;o de mesclagem | Microsoft Docs"
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
  - "recuperação [replicação do SQL Server], replicação de mesclagem"
  - "backups [replicação do SQL Server], replicação de mesclagem"
  - "restauração [replicação do SQL Server], replicação de mesclagem"
  - "replicação de mesclagem [replicação do SQL Server], backup e restauração"
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 48
---
# Estrat&#233;gias para fazer backup e restaurar a replica&#231;&#227;o de mesclagem
  Para replicação de mesclagem, faça backup dos seguintes bancos de dados regularmente:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   O **mestre** e **msdb** bancos de dados do sistema no publicador, distribuidor e todos os assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça backup do **mestre** e **msdb** bancos de dados no publicador ao mesmo tempo você faça backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, certifique-se de que o **mestre** e **msdb** banco de dados são consistentes com o banco de dados em termos de configuração de replicação e as configurações de publicação.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se você não executar backups de log, um backup deverá ser executado sempre que uma configuração relevante à replicação for alterada. Para obter mais informações, consulte [ações comuns que requerem um Backup atualizado](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
 Escolha uma das abordagens descritas abaixo, para fazer o backup e a restauração do banco de dados de publicação, e, então, siga as recomendações relacionadas abaixo, para o banco de dados de publicação e para os bancos de dados de assinaturas.  
  
## Fazendo backup e restaurando o banco de dados de publicação  
 Há duas abordagens para restaurar um banco de dados de publicação de mesclagem. Depois de restaurar o banco de dados de publicação de um backup, você deverá:  
  
-   Sincronizar o banco de dados de publicação com um banco de dados de assinatura.  
  
-   Reinicializar todas as assinaturas para publicações no banco de dados de publicação.  
  
 Usar qualquer um desses métodos garante que, depois que uma restauração é executada, o Publicador e todos os Assinantes serão sincronizados.  
  
> [!NOTE]  
>  Se qualquer tabela contiver colunas de identidade, você deve certificar-se que os intervalos corretos de identidade estão atribuídos, depois de uma restauração. Para obter mais informações, consulte [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### Sincronizando o banco de dados de publicação  
 Sincronizar um banco de dados de publicação com um banco de dados de assinatura permitirá a você carregar a partir de um ou mais bancos de dados de assinatura, as mudanças que foram feitas anteriormente no banco de dados de publicação, mas que não foram representadas no backup restaurado. Os dados que podem ser carregados dependem do modo como uma publicação é filtrada:  
  
-   Se a publicação não for filtrada, você deverá conseguir atualizar o banco de dados de publicação com uma sincronização com o Assinante mais atualizado.  
  
-   Se a publicação for filtrada, talvez você possa atualizar o banco de dados de publicação. Considere uma tabela particionada, de modo que cada assinatura receba os dados de clientes somente de uma região: norte, leste, sul e oeste. Se existir pelo menos um Assinante para cada partição de dados, a sincronização com um Assinante para cada partição deverá atualizar o banco de dados de publicação. Entretanto, se por exemplo, os dados da partição oeste, não foram replicados para nenhum Assinante, então esses dados no Publicador não poderão ser atualizados.  
  
> [!IMPORTANT]  
>  Sincronizar um banco de dados de publicação com um banco de dados de assinatura pode resultar em tabelas publicadas restauradas a um point-in-time, que é mais recente que o point-in-time de outras tabelas não publicadas, que foram restaurados a partir do backup.  
  
 Se você sincronizar com um assinante que está executando uma versão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], a assinatura não poderá ser anônima; ele deve ser uma assinatura de cliente ou servidor (conhecido como assinaturas locais e assinaturas globais nas versões anteriores).  
  
 Para sincronizar uma assinatura, consulte [sincronizar uma assinatura Push](../../../relational-databases/replication/synchronize-a-push-subscription.md) e [sincronizar uma assinatura Pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
### Reinicializando todas as assinaturas  
 Reinicializar todas as assinatura assegura que todos os Assinantes estarão em um estado consistente com o banco de dados de publicação restaurado. Essa abordagem deverá ser usada se desejar retornar uma topologia inteira ao estado anterior, representado por um determinado backup de banco de dados de publicação. Por exemplo, é possível reinicializar todas as assinaturas, se estiver restaurando um banco de dados de publicação a partir de um point-in-time especifico, como um mecanismo de recuperação para uma operação em lote executada erroneamente.  
  
 Se você escolher essa opção, gere um instantâneo novo para entregar aos Assinantes reinicializados, imediatamente depois de restaurar seu banco de dados de publicação.  
  
 Para reinicializar uma assinatura, consulte [reinicializar uma assinatura](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
 Para criar e aplicar um instantâneo, consulte [criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) e [criar um instantâneo para uma publicação de mesclagem com filtros parametrizados](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## Fazendo backup e restaurando o banco de dados de distribuição  
 Com a replicação de mesclagem, deve ser realizado regularmente o backup do banco de dados de distribuição, e, pode ser restaurado sem nenhuma consideração especial, contanto que o backup usado não seja anterior ao menor período de retenção de todas as publicações que usam o Distribuidor. Por exemplo, se houver três publicações com períodos de retenção de 10, 20, e 30 dias, respectivamente, o backup usado para restaurar o banco de dados não deve ter mais de 10 dias. O banco de dados de distribuição tem uma função limitada na replicação de mesclagem: não armazena nenhum dos dados usados no controle de alterações e não fornece o armazenamento temporário das mudanças de replicação de mesclagem a serem encaminhadas aos bancos de dados de assinatura (como faz na replicação transacional).  
  
## Fazendo backup e restaurando um banco de dados de assinatura  
 Para garantir a recuperação bem sucedida de um banco de dados de assinantes, os assinantes devem sincronizar com o Publicador, antes que tenha sido realizado o backup do banco de dados de assinatura; devem também sincronizar depois que o banco de dados de assinatura é restaurado:  
  
-   Sincronizar com o Publicador, antes que tenha sido realizado o backup do banco de dados de assinatura ajuda a garantir que, se um Assinante é restaurado a partir do backup, a assinatura ainda estará dentro do período de retenção da publicação: Por exemplo, imagine uma publicação com um período de retenção de 10 dias. A última sincronização foi há 8 dias e o backup é realizado agora. Se o backup for realizado 4 dias depois, a última sincronização terá ocorrido há 12 dias, antes do período de retenção. Nesse caso, você teria de reinicializar o Assinante. Se o Assinante tivesse sincronizado antes do backup, o banco de dados de assinatura estaria dentro do período de retenção.  
  
     O backup não deve ser anterior ao menor período de retenção de todas as publicações assinadas pelo Assinante. Por exemplo, se o Assinante assinar três publicações com períodos de retenção de 10, 20, e 30 dias, respectivamente, o backup usado para restaurar o banco de dados não deve ter mais de 10 dias.  
  
-   Sincronizar o banco de dados de assinatura com cada uma de suas publicações, depois de uma restauração, garante que o Assinante está atualizado com todas as alterações do Publicador.  
  
 Para definir o período de retenção da publicação, consulte [definir o período de validade para assinaturas](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
 Para sincronizar uma assinatura, consulte [sincronizar uma assinatura Push](../../../relational-databases/replication/synchronize-a-push-subscription.md) e [sincronizar uma assinatura Pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## Fazendo backup e restaurando um banco de dados de republicação  
 Quando um banco de dados assina os dados de um Publicador e, por sua vez, publica os mesmos dados em outros bancos de dados de assinatura, isso é chamado de banco de dados de republicação. Ao restaurar um banco de dados de republicação, siga as diretrizes descritas em "Fazendo backup e restaurando um banco de dados de publicação" e "Fazendo backup e restaurando um banco de dados de assinatura" neste tópico.  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  