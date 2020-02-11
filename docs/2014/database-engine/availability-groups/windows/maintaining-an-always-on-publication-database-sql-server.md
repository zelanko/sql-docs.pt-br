---
title: Mantendo um banco de dados de publicação AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a862c5c9cea1087f54a4dbff13b6c39eb5e39385
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62791948"
---
# <a name="maintaining-an-alwayson-publication-database-sql-server"></a>Mantendo um banco de dados de publicação AlwaysOn (SQL Server)
  Este tópico discute considerações especiais para manter um banco de dados de publicação quando você usa grupos de disponibilidade AlwaysOn.  
  
 
  
##  <a name="MaintainPublDb"></a> Mantendo um banco de dados publicado em um grupo de disponibilidade  
 Manter um banco de dados de publicação AlwaysOn é basicamente o mesmo que manter um banco de dados de publicação padrão, com as seguintes considerações:  
  
-   A administração deve ocorrer no host de réplica primária. No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], as publicações aparecem sob a pasta **Publicações Locais** para o host de réplica primária e também para réplicas secundárias legíveis. Depois do failover, talvez você precise atualizar manualmente o [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] para que a alteração seja refletida se a réplica secundária elevada a primária não estiver legível.  
  
-   O monitor de replicação sempre exibe informações de publicação sob o publicador original. Entretanto, estas informações podem ser exibidas no Monitor de Replicação de qualquer réplica, adicionando o publicador original como um servidor.  
  
-   Ao usar os procedimentos armazenados ou RMO (Replication Management Objects) para gerenciar na réplica primária atual, nos casos em que você especifica o nome do Publicador, especifique o nome da instância na qual o banco de dados foi habilitado para a replicação (o publicador original). Para determinar o nome apropriado, use a função `PUBLISHINGSERVERNAME`. Quando um banco de dados de publicação ingressa em um grupo de disponibilidade, os metadados de replicação armazenados nas réplicas de banco de dados secundárias são idênticos aos da réplica primária. Portanto, para os bancos de dados de publicação habilitados para replicação na réplica primária, o nome da instância do publicador armazenado em tabelas do sistema na réplica secundária é o nome da réplica primária, e não da secundária. Isso afeta a configuração e a manutenção da replicação, em caso de falha do banco de dados de publicação para uma réplica secundária. Por exemplo, se você estiver configurando a replicação com procedimentos armazenados em um secundário após o failover e quiser uma assinatura pull para um banco de dados de publicação que foi habilitado em uma réplica diferente, deverá especificar o nome do Publicador original em vez do *@publisher* Publicador `sp_addpullsubscription` atual `sp_addmergepulllsubscription`como o parâmetro de ou. Entretanto, se você habilitar um banco de dados de publicação depois do failover, o nome de instância de publicador armazenado nas tabelas do sistema será o nome do host primário atual. Nesse caso, você usaria o nome do host da réplica primária atual para o *@publisher* parâmetro.  
  
    > [!NOTE]  
    >  Para alguns procedimentos, como `sp_addpublication`, o *@publisher* parâmetro tem suporte apenas para Publicadores que não são instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; nesses casos, ele não é relevante para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o AlwaysOn.  
  
-   Para sincronizar uma assinatura no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] após o failover, sincronize as assinaturas pull do assinante e sincronize as assinaturas push do publicador ativo.  
  
##  <a name="RemovePublDb"></a> Removendo um banco de dados publicado de um grupo de disponibilidade  
 Considere os problemas a seguir se um banco de dados publicado for removido de um grupo de disponibilidade, ou se um grupo de disponibilidade que tem um banco de dados de membro publicado for removido.  
  
-   Se o banco de dados de publicação no Publicador original for removido de uma réplica primária do grupo de `sp_redirect_publisher` disponibilidade, você deverá executar sem *@redirected_publisher* especificar um valor para o parâmetro a fim de remover o redirecionamento do par Publicador/banco de dados.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     O banco de dados será deixado no estado de recuperação na réplica primária e deve ser restaurado. Quando você faz isso, a replicação deve funcionar inalterada no Publicador original.  
  
-   Se o banco de dados de publicação falhar no publicador original para uma réplica e o banco de dados for removido da réplica primária de grupo de disponibilidade, use o procedimento armazenado `sp_redirect_publisher` para redirecionar explicitamente o publicador original para o novo publicador. O banco de dados será deixado no estado de recuperação e deverá ser restaurado. Quando você faz isso, a replicação deve continuar a funcionar como ocorria no grupo de disponibilidade.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     Não remova o servidor remoto para o publicador original do distribuidor, mesmo que o servidor não possa mais ser acessado. Os metadados de servidor para o publicador original são necessários no distribuidor para atender consultas de metadados de publicação.  
  
-   Se um grupo de disponibilidade completo for removido, o comportamento em relação a um banco de dados replicado de membro será igual ao de um banco de dados publicado que é removido de um grupo de disponibilidade. A replicação poderá ser retomada da réplica primária mais recente assim que o banco de dados for restaurado e o redirecionamento for modificado. Se o banco de dados for restaurado em seu publicador original, o redirecionamento deverá ser removido. Se o banco de dados for restaurado em um host diferente, o redirecionamento deverá ser direcionado explicitamente ao novo host.  
  
    > [!NOTE]  
    >  Quando um grupo de disponibilidade que publicou bancos de dados de membro é removido, ou um banco de dados publicado é removido de um grupo de disponibilidade, todas as cópias dos bancos de dados publicados permanecem no estado de recuperação. Se restaurado, cada um aparecerá como um banco de dados publicado. Apenas uma cópia deve ser retida com metadados de publicação. Para desabilitar a replicação para uma cópia de banco de dados publicada, primeiro remova todas as assinaturas e publicações do banco de dados.  
  
     Execute `sp_dropsubscription` para remover assinaturas da publicação. Certifique-se de definir o *@ignore_distributributor* parâmetro como 1 para preservar os metadados do banco de dados de publicação ativa no distribuidor.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     Execute `sp_droppublication` para remover todas as publicações. Novamente, defina o parâmetro *@ignore_distributor* como 1 para preservar os metadados do banco de dados de publicação ativa no distribuidor.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     Execute `sp_replicationdboption` para desabilitar a replicação para o banco de dados.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     Neste momento, a cópia do banco de dados publicado pode ser retida ou removida.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar a replicação para grupos de disponibilidade AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)  
  
-   [Replicação, Controle de Alterações, captura de dados de alteração e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Perguntas Frequentes sobre Administração de Replicação](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
-   [Assinantes de replicação e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de Disponibilidade AlwaysOn: interoperabilidade (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Replicação do SQL Server](../../../relational-databases/replication/sql-server-replication.md)  
  
  
