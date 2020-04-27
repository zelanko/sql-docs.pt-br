---
title: Excluir um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffda3be2194b26b46f9633c3bdf76d60d36ce73c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871908"
---
# <a name="delete-a-database"></a>Excluir um banco de dados
  Este tópico descreve como excluir um banco de dados definido pelo usuário no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para excluir um diagrama de banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [após excluir um banco de dados](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Bancos de dados de sistema não podem ser excluídos.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Exclua todos os instantâneos do banco de dados que existam no banco de dados. Para obter mais informações, veja [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
-   Se o banco de dados estiver envolvido em envio de logs, remova o envio do logs.  
  
-   Se o banco de dados for publicado para replicação transacional, publicado ou com assinatura para replicação de mesclagem, remova a replicação do banco de dados.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Pense em fazer um backup completo do banco de dados. Um banco de dados excluído só poderá ser recriado por meio da restauração de um backup.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para executar DROP DATABASE, a um mínimo, um usuário deve ter permissão CONTROL no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-database"></a>Para excluir um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados para excluí-lo e depois clique em **Excluir**.  
  
3.  Confirme se o banco de dados correto está selecionado e depois clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
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
  
##  <a name="follow-up-after-deleting-a-database"></a><a name="FollowUp"></a> Acompanhamento: após excluir um banco de dados  
 Faça backup do banco de dados **mestre** . Se o **mestre** precisar ser restaurado, todos os bancos de dados que tiverem sido excluídos desde o último backup do **mestre** ainda terão referências nas exibições do catálogo do sistema e poderão gerar mensagens de erro.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
