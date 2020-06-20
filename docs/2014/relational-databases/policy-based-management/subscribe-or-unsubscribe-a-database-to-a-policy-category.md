---
title: Assinar ou cancelar a assinatura de um banco de dados a uma categoria de política | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2b4ca6f804352b57b30b42012da93e0d031be8d4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066636"
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>Assinar ou cancelar a assinatura de um banco de dados a uma categoria de política
  Este tópico descreve como assinar ou cancelar a assinatura de um banco de dados para uma categoria de política no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para assinar ou cancelar a assinatura de um banco de dados a uma categoria de política usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>Para assinar ou cancelar a assinatura de um banco de dados a uma categoria de política  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o banco de dados em que você deseja gerenciar assinaturas de categoria.  
  
2.  Clique no sinal de adição para expandir a pasta **Bancos de dados** .  
  
3.  Clique com o botão direito do mouse no banco de dados em que você deseja gerenciar assinaturas de categoria, aponte para **Políticas**e selecione **Categorias**  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Categorias** :  
  
     Expandir coluna  
     Clique para expandir uma categoria de política. Assim, todas as políticas incluídas na categoria serão listadas.  
  
     **Nome**  
     O nome da categoria de política.  
  
     **Assinado**  
     Indica se o destino se inscreveu na categoria de política. Se esta caixa de seleção for desabilitada, a categoria de política será definida como **Autorizar Assinaturas de Banco de Dados**. Isto significa que a categoria de política se aplica a todos os bancos de dados no servidor.  
  
     **Política**  
     Quando os grupos de políticas são expandidos, exibe as políticas da categoria de políticas.  
  
     **Enabled**  
     Indica se as políticas estão habilitadas ou desabilitadas.  
  
     **Modo de Execução**  
     Exibe o modo de execução da política.  
  
     **Histórico**  
     Clique no hiperlink Exibir Histórico para abrir o Visualizador do Arquivo de Log e ver o histórico de políticas.  
  
4.  Para assinar uma categoria de Gerenciamento Baseada em Políticas, marque a caixa de seleção de categoria na coluna **Assinado** . Para cancelar a assinatura de uma categoria, desmarque a caixa de seleção.  
  
5.  Ao concluir, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>Para assinar um banco de dados para uma categoria de política  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Para obter mais informações, veja [sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql).  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>Para cancelar a assinatura de um banco de dados para uma categoria de política  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Para obter mais informações, veja [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql).  
  
  
