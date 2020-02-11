---
title: Restaurar um banco de dados para uma transação marcada (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 919c10372e397f0c2d66d7648363aef7916ec598
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875607"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>Restaurar um banco de dados para uma transação marcada (SQL Server Management Studio)
  Quando um banco de dados está no estado de restauração, é possível usar a caixa de diálogo **Restaurar Log de Transações** para restaurar o banco de dados para uma transação marcada nos backups de log disponíveis.  
  
> [!NOTE]  
>  Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md) e [Recuperação de bancos de dados relacionados que contêm transação marcada](recovery-of-related-databases-that-contain-marked-transaction.md).  
  
### <a name="to-restore-a-marked-transaction"></a>Para restaurar uma transação marcada  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Restaurar**.  
  
4.  Clique em **Log de Transações**, o que abrirá a caixa de diálogo **Restaurar Log de Transações** .  
  
5.  Na página **Geral** , na seção **Restaurar para** , selecione **Transação marcada**, o que abrirá a caixa de diálogo **Selecionar Transação Marcada** . Essa caixa de diálogo exibe uma grade que lista as transações marcadas disponíveis nos backups de log de transações selecionados.  
  
     Por padrão, a restauração vai até a transação marcada, mas a exclui. Para restaurar também a transação marcada, selecione **Incluir transação marcada**.  
  
     A tabela a seguir lista os cabeçalhos de coluna da grade e descreve seus valores.  
  
    |Cabeçalho|Valor|  
    |------------|-----------|  
    |\<em branco>|Exibe uma caixa de seleção para selecionar a marca.|  
    |**Transaction Mark**|Nome da transação marcada especificado pelo usuário quando a transação foi confirmada.|  
    |**Data**|Data e hora de confirmação da transação. A data e hora da transação são exibidas como registradas na tabela **msdbgmarkhistory** , não a data e hora do computador cliente.|  
    |**Descrição**|Descrição da transação marcada especificada pelo usuário quando a transação foi confirmada (se houver).|  
    |**LSN**|Número de sequência de log da transação marcada.|  
    |**Backup de banco de dados**|Nome do banco de dados em que a transação marcada foi confirmada.|  
    |**Nome de usuário**|Nome do usuário do banco de dados que confirmou a transação marcada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar um backup de banco de dados &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
  
