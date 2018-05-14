---
title: Migrar as configurações de backup gerenciado do SQL Server 2014 para o SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 894fe1d91cd11ec111f9628206a543ab4f2cff40
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016"></a>Migrar as Configurações de Backup Gerenciado do SQL Server 2014 para o SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico aborda considerações sobre a migração para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] durante a atualização do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
 Os procedimentos e o comportamento subjacente do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] foram alterados no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. As seções a seguir descrevem as alterações funcionais e suas implicações.  
  
## <a name="overview"></a>Visão geral  
 A tabela a seguir descreve algumas das principais diferenças funcionais para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] entre o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
|Área|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
|----------|---------------------------|---------------------------|  
|**Namespace:**|smart_admin|managed_backup|  
|**Procedimentos armazenados do sistema:**|sp_set_db_backup<br /><br /> sp_set_instance_backup|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)<br /><br /> [sp_backup_config_advanced](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)<br /><br /> [sp_backup_config_schedule](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|  
|**Segurança:**|Credencial do SQL que usa uma chave de acesso e uma conta de armazenamento do Microsoft Azure.|Credencial do SQL que usa um token de assinatura de acesso compartilhado (SAS) do Microsoft Azure.|  
|**Armazenamento subjacente:**|Armazenamento do Microsoft Azure que usa blobs de página.|Armazenamento do Microsoft Azure que usa blobs de bloco.|  
  
## <a name="benefits"></a>Benefícios  
 Há vários benefícios ao usar a nova funcionalidade no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
-   Os blobs de bloco custam menos para armazenar.  
  
-   Com a distribuição, você pode armazenar backups muito maiores (12 TB em vez de 1 TB para blobs de página).  
  
-   A distribuição também melhora o tempo de restauração para bancos de dados grandes  
  
-   Para ver outras melhorias ao [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], confira [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="considerations"></a>Considerações  
 Após a atualização do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], observe as seguintes considerações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :  
  
-   Todos os bancos de dados configurados anteriormente para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] continuarão a usar os procedimentos do sistema do **smart_admin** e o comportamento subjacente no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
-   Os procedimentos do **smart_admin** não têm suporte para as novas configurações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. É necessário usar os novos procedimentos e a funcionalidade **managed_backup** .  
  
## <a name="see-also"></a>Consulte Também  
 [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
