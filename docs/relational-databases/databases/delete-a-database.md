---
title: Excluir um banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2b4f5a1c5a2f209ff8f9f933e49354b4c0952475
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="delete-a-database"></a>Excluir um banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como excluir um banco de dados definido pelo usuário no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para excluir um diagrama de banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After deleting a database](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Bancos de dados de sistema não podem ser excluídos.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Exclua todos os instantâneos do banco de dados que existam no banco de dados. Para obter mais informações, veja [Remover um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
-   Se o banco de dados estiver envolvido em envio de logs, remova o envio do logs.  
  
-   Se o banco de dados for publicado para replicação transacional, publicado ou com assinatura para replicação de mesclagem, remova a replicação do banco de dados.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Pense em fazer um backup completo do banco de dados. Um banco de dados excluído só poderá ser recriado por meio da restauração de um backup.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar DROP DATABASE, a um mínimo, um usuário deve ter permissão CONTROL no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-database"></a>Para excluir um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados para excluí-lo e depois clique em **Excluir**.  
  
3.  Confirme se o banco de dados correto está selecionado e depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-database"></a>Para excluir um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo remove os bancos de dados `Sales` e `NewSales` .  
  
```sql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de excluir um banco de dados  
 Faça backup do banco de dados **mestre** . Se o **mestre** precisar ser restaurado, todos os bancos de dados que tiverem sido excluídos desde o último backup do **mestre** ainda terão referências nas exibições do catálogo do sistema e poderão gerar mensagens de erro.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
