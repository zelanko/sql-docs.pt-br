---
title: Tarefa de limpeza de histórico (plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability"
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a0629aa0787b535f0a577c60751665d7a2dd760e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806798"
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
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)  
  
  
