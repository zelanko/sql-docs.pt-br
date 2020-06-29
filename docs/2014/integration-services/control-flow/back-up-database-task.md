---
title: Tarefa Backup de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0980d89cc915121414dd7d3c89be6f4d72eb715
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433993"
---
# <a name="back-up-database-task"></a>Tarefa de Backup de Banco de Dados
  A tarefa Backup de Banco de Dados executa vários tipos de backups de bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Usando a tarefa de Backup de Banco de Dados, um pacote poderá fazer backup de um único ou de vários bancos de dados. Se a tarefa fizer backup de um único banco de dados, você poderá escolher o componente de backup: o banco de dados ou seus arquivos e grupos de arquivos.  
  
## <a name="supported-recover-models-and-backup-types"></a>Modelos de recuperação e tipos de backup com suporte  
 A tabela a seguir relaciona os modelos de recuperação e tipos de backup que a tarefa de Backup de Banco de Dados oferece suporte.  
  
|modelo de recuperação|Banco de dados|Diferenciais de bancos de dados|Log de transações|Arquivo ou diferencial de arquivo|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simples|Obrigatório|Opcional|Sem suporte|Sem suporte|  
|Completo|Obrigatório|Opcional|Obrigatório|Opcional|  
|Bulk-logged|Obrigatório|Opcional|Obrigatório|Opcional|  
  
 A tarefa de Backup de Banco de Dados encapsula uma instrução BACKUP Transact-SQL. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Configuração da tarefa de Backup de Banco de Dados  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Backup de Banco de Dados &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
  
