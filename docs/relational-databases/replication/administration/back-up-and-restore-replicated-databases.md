---
title: "Fazer backup e restaurar bancos de dados replicados | Microsoft Docs"
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
  - "backups [replicação do SQL Server]"
  - "administrando a replicação, restaurando"
  - "fazendo backup de bancos de dados replicados"
  - "backups [replicação do SQL Server], sobre backups"
  - "restaurando bancos de dados replicados [replicação do SQL Server]"
  - "recuperação [replicação do SQL Server], sobre a recuperação"
  - "restaurando bancos de dados [SQL Server], bancos de dados replicados"
  - "fazendo backup de bancos de dados [SQL Server], bancos de dados replicados"
  - "restaurando [replicação do SQL Server], sobre a restauração"
  - "recuperação [replicação do SQL Server]"
  - "replicação [SQL Server], administrando"
  - "bancos de dados de distribuição [replicação do SQL Server], fazendo backup"
  - "restaurando [replicação do SQL Server]"
  - "administrando a replicação, fazendo backup"
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Fazer backup e restaurar bancos de dados replicados
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Bancos de dados replicados requerem atenção especial em relação a backup e restauração de dados. Este tópico fornece informações iniciais e links para obter mais informações sobre estratégias de backup e restauração para cada tipo de replicação.  
  
 A replicação oferece suporte à restauração de bancos de dados replicados para o mesmo servidor e banco de dados dos quais o backup foi criado. Se você restaurar um backup de um banco de dados replicado para outro servidor ou banco de dados, as configurações de replicação não poderão ser preservadas. Neste caso, você deve recriar todas as publicações e assinaturas depois que os backups forem restaurados.  
  
> [!NOTE]  
>  Será possível restaurar um banco de dados replicado para um servidor auxiliar se estiver sendo usada a remessa de log. Para obter mais informações, consulte [replicação e envio de logs e 40; SQL Server & 41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 Deve ser feito backup regularmente para bancos de dados replicados e bancos de dados do sistema associados. Faça backup dos seguintes bancos de dados:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   O **mestre** e **msdb** bancos de dados do sistema no publicador, distribuidor e todos os assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça backup do **mestre** e **msdb** bancos de dados no publicador ao mesmo tempo você faça backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, certifique-se de que o **mestre** e **msdb** banco de dados são consistentes com o banco de dados em termos de configuração de replicação e as configurações de publicação.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se não executar backups de log, um backup deve ser executado sempre que uma configuração pertinente à replicação for alterada. Para obter mais informações, consulte [ações comuns que requerem um Backup atualizado](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Estratégias de backup e restauração  
 As estratégias de backup e restauração de cada nó em uma topologia de replicação diferem de acordo com tipo de replicação usado. Para obter informações sobre estratégias de backup e restauração para cada tipo de replicação, consulte os tópicos abaixo:  
  
-   [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Estratégias para fazer backup e restaurar a replicação de mesclagem](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Como parte de qualquer estratégia de recuperação, mantenha sempre um script atual de suas configurações de replicação em um local seguro. No caso de uma falha do servidor ou da necessidade de configurar um ambiente de teste, você poderá modificar o script alterando as referências no nome do servidor e isso poderá ser usado para ajudar a recriar suas configurações de replicação. Além de executar o script em suas configurações de replicação atuais, você deve executar o script de habilitação e desabilitação da replicação. Para obter informações sobre scripts de objetos de replicação, consulte [scripts de replicação](../../../relational-databases/replication/scripting-replication.md).  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Práticas recomendadas para administração de replicação](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  