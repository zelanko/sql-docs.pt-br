---
title: Restaurar banco de dados para a transação marcada (SSMS)
description: Quando um banco de dados do SQL Server estiver sendo restaurado, use a caixa de diálogo Restaurar Log de Transações para restaurar o banco de dados para uma transação marcada nos backups de log disponíveis.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: cawrites
ms.author: chadam
ms.openlocfilehash: d35f1478d3d9f290557a6eeebd6ce4365e461e21
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129119"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>Restaurar um banco de dados para uma transação marcada (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Quando um banco de dados está no estado de restauração, é possível usar a caixa de diálogo **Restaurar Log de Transações** para restaurar o banco de dados para uma transação marcada nos backups de log disponíveis.  
  
> [!NOTE]  
>  Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) e [Recuperação de bancos de dados relacionados que contêm transação marcada](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
### <a name="to-restore-a-marked-transaction"></a>Para restaurar uma transação marcada  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados** e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas** e clique em **Restaurar**.  
  
4.  Clique em **Log de Transações**, o que abrirá a caixa de diálogo **Restaurar Log de Transações** .  
  
5.  Na página **Geral** , na seção **Restaurar para** , selecione **Transação marcada**, o que abrirá a caixa de diálogo **Selecionar Transação Marcada** . Essa caixa de diálogo exibe uma grade que lista as transações marcadas disponíveis nos backups de log de transações selecionados.  
  
     Por padrão, a restauração vai até a transação marcada, mas a exclui. Para restaurar também a transação marcada, selecione **Incluir transação marcada**.  
  
     A tabela a seguir lista os cabeçalhos de coluna da grade e descreve seus valores.  
  
    |Cabeçalho|Valor|  
    |------------|-----------|  
    |\<blank>|Exibe uma caixa de seleção para selecionar a marca.|  
    |**Transaction Mark**|Nome da transação marcada especificado pelo usuário quando a transação foi confirmada.|  
    |**Data**|Data e hora de confirmação da transação. A data e hora da transação são exibidas como registradas na tabela **msdbgmarkhistory** , não a data e hora do computador cliente.|  
    |**Descrição**|Descrição da transação marcada especificada pelo usuário quando a transação foi confirmada (se houver).|  
    |**LSN**|Número de sequência de log da transação marcada.|  
    |**Backup de banco de dados**|Nome do banco de dados em que a transação marcada foi confirmada.|  
    |**Nome de usuário**|Nome do usuário do banco de dados que confirmou a transação marcada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
