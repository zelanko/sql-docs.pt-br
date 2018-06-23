---
title: Configurar compactação de backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 394b0f6016cd0820142f958fba0ea69cb2db9a7d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008914"
---
# <a name="configure-backup-compression-sql-server"></a>Configurar compactação de backup (SQL Server)
  Na instalação, a compactação de backup é desativada por padrão. O comportamento padrão da compactação de backup é definido pela opção de configuração em nível de servidor **padrão de compactação de backup** . No entanto, você pode substituir o padrão do nível de servidor ao criar um único backup ou agendar uma série de backups rotineiros. Para alterar o padrão no nível do servidor, consulte [Exibir ou configurar a opção de configuração de servidor padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Substituir o padrão de compactação de backup  
 É possível alterar o comportamento de compactação de backup para um backup individual, um trabalho de backup ou uma configuração de envio de logs.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Para substituir o padrão de compactação de backup do servidor ao criar um backup, use WITH NO_COMPRESSION ou WITH COMPRESSION na instrução [BACKUP](/sql/t-sql/statements/backup-transact-sql).  
  
     Para uma configuração de envio de logs, é possível controlar o comportamento de compactação de backup de backups de log usando [sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Para obter informações sobre como exibir ou configurar opção de padrão de compactação de backup para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Exibir ou configurar a opção de configuração de servidor do padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     Você pode substituir o padrão de compactação de backup do servidor durante a criação de um backup especificando **Compactar backup** ou **Não compactar o backup** em qualquer uma das seguintes caixas de diálogo:  
  
    -   [Backup de Banco de Dados (página Opções)](back-up-database-backup-options-page.md)  
  
         Ao fazer backup de um banco de dados, é possível controlar a compactação de backup de um backup individual de banco de dados, arquivo ou log.  
  
    -   [Usar o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         O Assistente de Plano de Manutenção permite que você controle a compactação de backup para cada conjunto de backups de banco de dados ou de log, completos ou diferenciais, que você programou.  
  
    -   [Tarefa de backup de banco de dados](../../integration-services/control-flow/back-up-database-task.md)do SSIS (Integration Services)  
  
         É possível controlar o comportamento da compactação de backup ao criar um pacote para fazer backup de um único banco de dados ou de vários bancos de dados.  
  
    -   [Configurações de backup de log de transações do envio de log](../databases/log-shipping-transaction-log-backup-settings.md)  
  
         Você pode controlar o comportamento da compactação de backup de backups de log.  
  
  
## <a name="see-also"></a>Consulte também  
 [Compactação de backup &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
  
