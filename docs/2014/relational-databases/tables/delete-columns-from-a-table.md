---
title: Excluir colunas de uma tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 718aeca12c90435b68fd6cedde150dfbdeb3c063
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62761650"
---
# <a name="delete-columns-from-a-table"></a>Excluir colunas de uma tabela
  Este tópico descreve como excluir colunas de tabelas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Ao excluir uma coluna de uma tabela, ela e todos os dados que ela contém serão excluídos do banco de dados. Essa ação não pode ser desfeita.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir uma coluna de uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Você não pode excluir uma coluna que tenha uma restrição CHECK. Você deve excluir primeiramente a restrição.  
  
 Você não pode excluir uma coluna que tenha restrições PRIMARY KEY ou FOREIGN KEY ou outras dependências, exceto quando estiver usando o Designer de Tabela. No Pesquisador de Objetos ou no [!INCLUDE[tsql](../../includes/tsql-md.md)], você deve primeiramente remover todas as dependências da coluna.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-columns-by-using-object-explorer"></a>Para excluir colunas usando o Pesquisador de Objetos  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela da qual você deseja excluir colunas e selecione **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
 Se a coluna contiver restrições ou outras dependências, uma mensagem de erro será exibida na caixa de diálogo **Excluir Objeto** . Resolva o erro excluindo as restrições referenciadas.  
  
#### <a name="to-delete-columns-by-using-table-designer"></a>Para excluir colunas usando o Designer de Tabela  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela da qual você deseja excluir colunas e selecione **Design**.  
  
2.  Clique com o botão direito do mouse na coluna que deseja excluir e escolha **Excluir Coluna** no menu de atalho.  
  
3.  Se a coluna participar de uma relação (FOREIGN KEY ou PRIMARY KEY), uma mensagem solicitará que você confirme a exclusão das colunas selecionadas e suas relações. Escolha **Sim**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-columns"></a>Para excluir colunas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
    ```  
  
 Se a coluna contiver restrições ou outras dependências, uma mensagem de erro será retornada. Resolva o erro excluindo as restrições referenciadas.  
  
 Para obter exemplos adicionais, consulte [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
##  <a name="FollowUp"></a>  
