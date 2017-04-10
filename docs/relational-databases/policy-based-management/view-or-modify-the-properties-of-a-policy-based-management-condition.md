---
title: "Exibir ou modificar as propriedades de uma condi&#231;&#227;o de gerenciamento baseado em pol&#237;ticas | Microsoft Docs"
ms.custom: ""
ms.date: "10/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gerenciamento Baseado em Políticas, exibir condições da política"
  - "Gerenciamento Baseado em Políticas, modificar condições da política"
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Exibir ou modificar as propriedades de uma condi&#231;&#227;o de gerenciamento baseado em pol&#237;ticas
  Este tópico descreve como exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  

  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para exibir ou modificar as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a condição que você deseja exibir ou modificar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Condições** .  
  
5.  Clique com o botão direito do mouse na condição que você deseja exibir ou editar e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Abrir Condição –***nome_condição*, veja [Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md), [Caixa de diálogo Abrir Condição, Página Políticas Dependentes](../../relational-databases/policy-based-management/open-condition-dialog-box-dependent-policies-page.md), [Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página de Descrição](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md) e [Caixa de diálogo Edição Avançada &#40;Condição&#41;](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para exibir as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [syspolicy_conditions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md).  
  
  