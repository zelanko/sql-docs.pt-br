---
title: "Restaurar um banco de dados para uma transação marcada (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 48529229420d7c2dafad334f3104e01add1a6746
ms.lasthandoff: 04/11/2017

---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>Restaurar um banco de dados para uma transação marcada (SQL Server Management Studio)
  Quando um banco de dados está no estado de restauração, é possível usar a caixa de diálogo **Restaurar Log de Transações** para restaurar o banco de dados para uma transação marcada nos backups de log disponíveis.  
  
> [!NOTE]  
>  Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) e [Recuperação de bancos de dados relacionados que contêm transação marcada](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
### <a name="to-restore-a-marked-transaction"></a>Para restaurar uma transação marcada  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Restaurar**.  
  
4.  Clique em **Log de Transações**, o que abrirá a caixa de diálogo **Restaurar Log de Transações** .  
  
5.  Na página **Geral** , na seção **Restaurar para** , selecione **Transação marcada**, o que abrirá a caixa de diálogo **Selecionar Transação Marcada** . Essa caixa de diálogo exibe uma grade que lista as transações marcadas disponíveis nos backups de log de transações selecionados.  
  
     Por padrão, a restauração vai até a transação marcada, mas a exclui. Para restaurar também a transação marcada, selecione **Incluir transação marcada**.  
  
     A tabela a seguir lista os cabeçalhos de coluna da grade e descreve seus valores.  
  
    |Cabeçalho|Value|  
    |------------|-----------|  
    |\<em branco>|Exibe uma caixa de seleção para selecionar a marca.|  
    |**Transaction Mark**|Nome da transação marcada especificado pelo usuário quando a transação foi confirmada.|  
    |**Data**|Data e hora de confirmação da transação. A data e hora da transação são exibidas como registradas na tabela **msdbgmarkhistory** , não a data e hora do computador cliente.|  
    |**Descrição**|Descrição da transação marcada especificada pelo usuário quando a transação foi confirmada (se houver).|  
    |**LSN**|Número de sequência de log da transação marcada.|  
    |**Banco de dados**|Nome do banco de dados em que a transação marcada foi confirmada.|  
    |**Nome do Usuário**|Nome do usuário do banco de dados que confirmou a transação marcada.|  
  
## <a name="see-also"></a>Consulte também  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
