---
title: Fazer backup de bancos de dados habilitados para Stretch (Stretch Database) | Microsoft Docs
ms.custom: 
ms.date: 06/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, backing up
- backups (Stretch Database)
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e28871ff432c9763b928293103e80468e37d69e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>Fazer backup de bancos de dados habilitados para Stretch (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 Os backups de banco de dados ajudam você a se recuperar de muitos tipos de desastres, erros e falhas.  
  
 -   Você precisa fazer backup de seus bancos de dados do SQL Server habilitados para Stretch.  
      
 -   O Microsoft Azure automaticamente faz backup dos dados remotos que o Stretch Database migrou do SQL Server para o Azure.  

> [!TIP]
> O backup é apenas uma parte de uma solução de continuidade dos negócios e de alta disponibilidade. Para obter mais informações sobre a alta disponibilidade, consulte [Soluções de alta disponibilidade](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).
   
## <a name="back-up-your-sql-server-data"></a>Fazer backup dos dados do SQL Server  
  
Para fazer backup de seus bancos de dados do SQL Server habilitados para Stretch, você pode continuar a usar os métodos de backup do SQL Server usados atualmente. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).
  
 Os backups de um banco de dados do SQL Server habilitados para Stretch contêm apenas dados locais e dados qualificados para migração no momento em que o backup é executado. (Dados qualificados são aqueles que ainda não foram migrados, mas serão migrados para o Azure com base nas configurações de migração das tabelas.) Isso é conhecido como um backup **superficial** e não inclui os dados já migrados para o Azure.  
  
## <a name="back-up-your-remote-azure-data"></a>Fazer backup dos dados do Azure remotos   
  
O Microsoft Azure automaticamente faz backup dos dados remotos que o Stretch Database migrou do SQL Server para o Azure.    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>O Azure reduz o risco de perda de dados com o backup automático  
O serviço SQL Server Stretch Database no Azure protege seus bancos de dados remotos com instantâneos de armazenamento automáticos pelo menos a cada 8 horas. Ele retém cada instantâneo por 7 dias para fornecer uma variedade de possíveis pontos de restauração.  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>O Azure reduz o risco de perda de dados com redundância geográfica  
Os backups de banco de dados do Azure são armazenados no Armazenamento do Azure com redundância geográfica (RA-GRS) e, portanto, com redundância geográfica por padrão. O armazenamento com redundância geográfica replica seus dados para uma região secundária a centenas de milhas de distância da região primária. Nas regiões primárias e secundárias, seus dados são replicados três vezes cada um, entre domínios de falha e domínios de atualização separados. Isso garante que seus dados sejam duráveis mesmo no caso de uma interrupção regional completa ou um desastre que torna uma das regiões do Azure indisponível.

### <a name="stretchRPO"></a>O Stretch Database reduz o risco de perda de dados para os dados do Azure retendo temporariamente as linhas migradas
Depois que o Stretch Database migra as linhas qualificadas do SQL Server para o Azure, ele retém essas linhas na tabela de preparo pelo mínimo de 8 horas. Se você restaurar um backup do banco de dados do Azure, o Stretch Database usa as linhas salvas na tabela de preparo para reconciliar os bancos de dados do SQL Server e do Azure.

Depois de restaurar um backup dos dados do Azure, você precisa executar o procedimento armazenado [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para reconectar o banco de dados do SQL Server habilitado para Stretch ao banco de dados remoto do Azure. Quando você executa **sys.sp_rda_reauthorize_db**, o Stretch Database automaticamente reconcilia os bancos de dados do SQL Server e do Azure.

Para aumentar o número de horas de dados migrados que o Stretch Database retém temporariamente na tabela de preparo, execute o procedimento armazenado [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) e especifique um número de horas maior que 8. Para decidir a quantidade de dados para reter, considere os seguintes fatores:
-   A frequência dos backups automáticos do Azure (pelo menos a cada 8 horas).
-   O tempo necessário após um problema para reconhecer o problema e decidir restaurar um backup.
-   A duração da operação de restauração do Azure.

> [!NOTE]
> Aumentar a quantidade de dados que o Stretch Database retém temporariamente na tabela de preparo aumenta a quantidade de espaço necessária no SQL Server.

Para verificar o número de horas de dados migrados que o Stretch Database atualmente retém temporariamente na tabela de preparo, execute o procedimento armazenado [sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md).

## <a name="see-also"></a>Consulte Também  
[Restaurar bancos de dados habilitados para Stretch](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [Gerenciar e solucionar problemas no Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  
