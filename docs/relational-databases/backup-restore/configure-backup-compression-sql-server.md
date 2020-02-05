---
title: Configurar compactação de backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 73f1d6c4d65a9e581611ef439c79c41eb691e4c9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68076120"
---
# <a name="configure-backup-compression-sql-server"></a>Configurar compactação de backup (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Na instalação, a compactação de backup é desativada por padrão. O comportamento padrão da compactação de backup é definido pela opção de configuração em nível de servidor **padrão de compactação de backup** . No entanto, você pode substituir o padrão do nível de servidor ao criar um único backup ou agendar uma série de backups rotineiros. Para alterar o padrão no nível do servidor, consulte [Exibir ou configurar a opção de configuração de servidor padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Substituir o padrão de compactação de backup  
 É possível alterar o comportamento de compactação de backup para um backup individual, um trabalho de backup ou uma configuração de envio de logs.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Para substituir o padrão de compactação de backup do servidor ao criar um backup, use WITH NO_COMPRESSION ou WITH COMPRESSION na instrução [BACKUP](../../t-sql/statements/backup-transact-sql.md).  
  
     Para uma configuração de envio de logs, é possível controlar o comportamento de compactação de backup de backups de log usando [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Para obter informações sobre como exibir ou configurar opção de padrão de compactação de backup para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Exibir ou configurar a opção de configuração de servidor do padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     Você pode substituir o padrão de compactação de backup do servidor durante a criação de um backup especificando **Compactar backup** ou **Não compactar o backup** em qualquer uma das seguintes caixas de diálogo:  
  
    -   [Backup de Banco de Dados (página Opções)](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)  
  
         Ao fazer backup de um banco de dados, é possível controlar a compactação de backup de um backup individual de banco de dados, arquivo ou log.  
  
    -   [Usar o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         O Assistente de Plano de Manutenção permite que você controle a compactação de backup para cada conjunto de backups de banco de dados ou de log, completos ou diferenciais, que você programou.  
  
    -   [Tarefa de backup de banco de dados](../../integration-services/control-flow/back-up-database-task.md)do SSIS (Integration Services)  
  
         É possível controlar o comportamento da compactação de backup ao criar um pacote para fazer backup de um único banco de dados ou de vários bancos de dados.  
  
    -   [Configurações de backup de log de transações do envio de log](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)  
  
         Você pode controlar o comportamento da compactação de backup de backups de log.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Compactação de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
