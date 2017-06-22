---
title: Excluir um procedimento armazenado | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9f9d65d2521299d34188897fbbf5675b5c9eea4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-stored-procedure"></a>Excluir um procedimento armazenado
    
##  <a name="Top"></a> Este tópico descreve como excluir um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Before you begin:**  [Limitations and Restrictions](#Restrictions), [Security](#Security)  
  
-   **To delete a procedure, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Excluir um procedimento pode causar a falha em objetos e scripts dependentes quando os objetos e scripts não são atualizados para refletir a remoção do procedimento. Entretanto, se um novo procedimento com o mesmo nome e o mesmo parâmetro for criado para substituir aquele que foi excluído, os outros objetos que o referenciam ainda serão processados com êxito. Para obter mais informações, veja [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer permissão ALTER no esquema ao qual o procedimento pertence ou permissão CONTROL no procedimento.  
  
##  <a name="Procedures"></a> Como excluir um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para excluir um procedimento no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda essa instância.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento a excluir e, depois, clique em **Excluir**.  
  
4.  Para exibir objetos que dependem do procedimento, clique em **Mostrar Dependências**.  
  
5.  Confirme se o procedimento correto está selecionado e, depois, clique em **OK**.  
  
6.  Remova as referências ao procedimento de quaisquer objetos e scripts dependentes.  
  
###  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para excluir um procedimento no Editor de Consultas**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de dados**, expanda o banco de dados ao qual o procedimento pertence, ou, da barra de ferramentas, selecione o banco de dados da lista de bancos de dados disponíveis.  
  
3.  No menu Arquivo, clique em **Nova Consulta**.  
  
4.  Obtenha o nome do procedimento armazenado a ser removido no banco de dados atual. No Pesquisador de Objetos, expanda **Programação** e, depois, expanda **Procedimentos Armazenados**. Outra alternativa é executar a instrução a seguir no editor de consultas.  
  
    ```tsql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  Copie e cole o exemplo a seguir no editor de consultas e insira um nome de procedimento armazenado a ser excluído do banco de dados atual.  
  
    ```tsql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  Remova as referências ao procedimento de quaisquer objetos e scripts dependentes.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Renomear um procedimento armazenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Exibir a definição de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
