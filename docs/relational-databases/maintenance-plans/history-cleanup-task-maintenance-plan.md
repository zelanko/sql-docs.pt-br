---
title: "Tarefa de limpeza de histórico (plano de manutenção) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbf4cfd2254dbe3e5f482e603ca7535682102d80
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="history-cleanup-task-maintenance-plan"></a>Tarefa limpeza de histórico (Plano de manutenção)
  Use a caixa de diálogo **Tarefa Limpeza de Histórico** para descartar informações antigas de histórico de tabelas no banco de dados msdb. Essa tarefa oferece suporte a exclusão de backup e restauração de histórico, histórico de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e histórico do plano de manutenção.  
  
 Essa instrução usa as instruções **sp_purge_jobhistory** e **sp_delete_backuphistory** .  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Nova**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita mais abaixo neste tópico.  
  
 **Histórico de backup e restauração**  
 A retenção de registros de quando foram criados backups recentes pode ajudar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criar um plano de recuperação quando você desejar restaurar um banco de dados. O período de retenção deve ser pelo menos a frequência de backups de banco de dados completos.  
  
 **Histórico de trabalho do SQL Server Agent**  
 Esse histórico pode ajudar a solucionar problemas de trabalhos com falha ou a determinar por que ações de banco de dados ocorreram.  
  
 **Histórico do plano de manutenção**  
 Esse histórico pode ajudar a solucionar problemas de trabalhos de plano de manutenção com falha ou a determinar por que ações de banco de dados ocorreram.  
  
 **Remover dados históricos com mais de**  
 Especifique a idade de itens que deseja excluir.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte a uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] com Autenticação do Microsoft Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte a uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] que usa a Autenticação do SQL Server. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte também  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  
