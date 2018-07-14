---
title: Estratégias para fazer backup e restaurar a replicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
caps.latest.revision: 47
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7dc8ba806b55f324c35a1573066e3c7e0f9372f7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230826"
---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>Estratégias para fazer backup e restaurar a replicação de mesclagem
  Para replicação de mesclagem, faça backup dos seguintes bancos de dados regularmente:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   Os bancos de dados de sistema **mestre** e **msdb** no Publicador, Distribuidor e todos os Assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça o backup dos bancos de dados **mestre** e **msdb** no Publicador ao mesmo tempo em que executa o backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, assegure-se de que os bancos de dados **mestre** e **msdb** são consistentes com o banco de dados de publicação, em termos de configuração de replicação e ajustes.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se você não executar backups de log, um backup deverá ser executado sempre que uma configuração relevante à replicação for alterada. Para obter mais informações, consulte [Ações comuns que requerem um backup atualizado](common-actions-requiring-an-updated-backup.md).  
  
 Escolha uma das abordagens descritas abaixo, para fazer o backup e a restauração do banco de dados de publicação, e, então, siga as recomendações relacionadas abaixo, para o banco de dados de publicação e para os bancos de dados de assinaturas.  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>Fazendo backup e restaurando o banco de dados de publicação  
 Há duas abordagens para restaurar um banco de dados de publicação de mesclagem. Depois de restaurar o banco de dados de publicação de um backup, você deverá:  
  
-   Sincronizar o banco de dados de publicação com um banco de dados de assinatura.  
  
-   Reinicializar todas as assinaturas para publicações no banco de dados de publicação.  
  
 Usar qualquer um desses métodos garante que, depois que uma restauração é executada, o Publicador e todos os Assinantes serão sincronizados.  
  
> [!NOTE]  
>  Se qualquer tabela contiver colunas de identidade, você deve certificar-se que os intervalos corretos de identidade estão atribuídos, depois de uma restauração. Para obter mais informações, consulte [Replicar colunas de identidade](../publish/replicate-identity-columns.md).  
  
### <a name="synchronizing-the-publication-database"></a>Sincronizando o banco de dados de publicação  
 Sincronizar um banco de dados de publicação com um banco de dados de assinatura permitirá a você carregar a partir de um ou mais bancos de dados de assinatura, as mudanças que foram feitas anteriormente no banco de dados de publicação, mas que não foram representadas no backup restaurado. Os dados que podem ser carregados dependem do modo como uma publicação é filtrada:  
  
-   Se a publicação não for filtrada, você deverá conseguir atualizar o banco de dados de publicação com uma sincronização com o Assinante mais atualizado.  
  
-   Se a publicação for filtrada, talvez você possa atualizar o banco de dados de publicação. Considere uma tabela particionada, de modo que cada assinatura receba os dados de clientes somente de uma região: norte, leste, sul e oeste. Se existir pelo menos um Assinante para cada partição de dados, a sincronização com um Assinante para cada partição deverá atualizar o banco de dados de publicação. Entretanto, se por exemplo, os dados da partição oeste, não foram replicados para nenhum Assinante, então esses dados no Publicador não poderão ser atualizados.  
  
> [!IMPORTANT]  
>  Sincronizar um banco de dados de publicação com um banco de dados de assinatura pode resultar em tabelas publicadas restauradas a um point-in-time, que é mais recente que o point-in-time de outras tabelas não publicadas, que foram restaurados a partir do backup.  
  
 Se você sincronizar com um Assinante que está executando uma versão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], então a assinatura não poderá ser anônima; deverá ser uma assinatura de cliente ou de servidor (chamadas de assinaturas locais e assinaturas globais nas versões anteriores).  
  
 Para sincronizar uma assinatura, consulte [Sincronizar uma assinatura push](../synchronize-a-push-subscription.md) e [Sincronizar uma assinatura pull](../synchronize-a-pull-subscription.md).  
  
### <a name="reinitializing-all-subscriptions"></a>Reinicializando todas as assinaturas  
 Reinicializar todas as assinatura assegura que todos os Assinantes estarão em um estado consistente com o banco de dados de publicação restaurado. Essa abordagem deverá ser usada se desejar retornar uma topologia inteira ao estado anterior, representado por um determinado backup de banco de dados de publicação. Por exemplo, é possível reinicializar todas as assinaturas, se estiver restaurando um banco de dados de publicação a partir de um point-in-time especifico, como um mecanismo de recuperação para uma operação em lote executada erroneamente.  
  
 Se você escolher essa opção, gere um instantâneo novo para entregar aos Assinantes reinicializados, imediatamente depois de restaurar seu banco de dados de publicação.  
  
 Para reinicializar uma assinatura, consulte [Reinicializar uma assinatura](../reinitialize-a-subscription.md).  
  
 Para criar e aplicar um instantâneo, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md) e [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>Fazendo backup e restaurando o banco de dados de distribuição  
 Com a replicação de mesclagem, deve ser realizado regularmente o backup do banco de dados de distribuição, e, pode ser restaurado sem nenhuma consideração especial, contanto que o backup usado não seja anterior ao menor período de retenção de todas as publicações que usam o Distribuidor. Por exemplo, se houver três publicações com períodos de retenção de 10, 20, e 30 dias, respectivamente, o backup usado para restaurar o banco de dados não deve ter mais de 10 dias. O banco de dados de distribuição tem uma função limitada na replicação de mesclagem: não armazena nenhum dos dados usados no controle de alterações e não fornece o armazenamento temporário das mudanças de replicação de mesclagem a serem encaminhadas aos bancos de dados de assinatura (como faz na replicação transacional).  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>Fazendo backup e restaurando um banco de dados de assinatura  
 Para garantir a recuperação bem sucedida de um banco de dados de assinantes, os assinantes devem sincronizar com o Publicador, antes que tenha sido realizado o backup do banco de dados de assinatura; devem também sincronizar depois que o banco de dados de assinatura é restaurado:  
  
-   Sincronizar com o Publicador, antes que tenha sido realizado o backup do banco de dados de assinatura ajuda a garantir que, se um Assinante é restaurado a partir do backup, a assinatura ainda estará dentro do período de retenção da publicação: Por exemplo, imagine uma publicação com um período de retenção de 10 dias. A última sincronização foi há 8 dias e o backup é realizado agora. Se o backup for realizado 4 dias depois, a última sincronização terá ocorrido há 12 dias, antes do período de retenção. Nesse caso, você teria de reinicializar o Assinante. Se o Assinante tivesse sincronizado antes do backup, o banco de dados de assinatura estaria dentro do período de retenção.  
  
     O backup não deve ser anterior ao menor período de retenção de todas as publicações assinadas pelo Assinante. Por exemplo, se o Assinante assinar três publicações com períodos de retenção de 10, 20, e 30 dias, respectivamente, o backup usado para restaurar o banco de dados não deve ter mais de 10 dias.  
  
-   Sincronizar o banco de dados de assinatura com cada uma de suas publicações, depois de uma restauração, garante que o Assinante está atualizado com todas as alterações do Publicador.  
  
 Para definir o período de retenção da publicação, consulte [Definir o período de expiração para assinaturas](../publish/set-the-expiration-period-for-subscriptions.md).  
  
 Para sincronizar uma assinatura, consulte [Sincronizar uma assinatura push](../synchronize-a-push-subscription.md) e [Sincronizar uma assinatura pull](../synchronize-a-pull-subscription.md).  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>Fazendo backup e restaurando um banco de dados de republicação  
 Quando um banco de dados assina os dados de um Publicador e, por sua vez, publica os mesmos dados em outros bancos de dados de assinatura, isso é chamado de banco de dados de republicação. Ao restaurar um banco de dados de republicação, siga as diretrizes descritas em "Fazendo backup e restaurando um banco de dados de publicação" e "Fazendo backup e restaurando um banco de dados de assinatura" neste tópico.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e Restauração de bancos de dados do SQL Server](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](back-up-and-restore-replicated-databases.md)  
  
  
