---
title: Conceder permissões em um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], permissions
ms.assetid: a7d15816-a788-4099-ad91-dc4b26618299
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47b8e4b87ab3150ae7bf67d3c3a2f9c5e0732294
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63015564"
---
# <a name="grant-permissions-on-a-stored-procedure"></a>Conceder permissões em um procedimento armazenado
  Este tópico descreve como conceder permissões em um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. As permissões podem ser concedidas a um usuário existente, a uma função de banco de dados ou a uma função de aplicativo no banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para conceder permissões em um procedimento armazenado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Não é possível usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para conceder permissões nos procedimentos do sistema ou funções do sistema. Em vez disso, use [Permissões do objeto GRANT](/sql/t-sql/statements/grant-object-permissions-transact-sql) .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita. Requer permissão ALTER no esquema ao qual o procedimento pertence ou permissão CONTROL no procedimento. Para obter mais informações, veja [Permissões de objeto GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>Para conceder permissões em um procedimento armazenado  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento para conceder permissões e clique em **Propriedades**.  
  
4.  De **Propriedades do Procedimento Armazenado**, selecione a página **Permissões** .  
  
5.  Para conceder permissões a um usuário, a uma função de banco de dados ou a uma função de aplicativo, clique em **Pesquisar**.  
  
6.  Em **Selecionar Usuários ou Funções**, clique em **Tipos de Objeto** para adicionar ou desmarcar os usuários ou funções que desejar.  
  
7.  Clique em **Procurar** para exibir a lista de usuários ou funções. Selecione os usuários ou funções aos quais as permissões devem ser concedidas.  
  
8.  Na grade **Permissões Explícitas** , selecione as permissões para concedê-las ao usuário especificado ou função. Para obter uma descrição das permissões, veja [Permissões &#40;Mecanismo de Banco de Dados&#41;](../security/permissions-database-engine.md).  
  
 Ao selecionar **Conceder** , uma permissão específica será dada ao beneficiado. Ao selecionar **Conceder Com** o beneficiado também poderá conceder a permissão específica a outros principais.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>Para conceder permissões em um procedimento armazenado  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo concede a permissão `EXECUTE` no procedimento armazenado `HumanResources.uspUpdateEmployeeHireInfo` para uma função de aplicativo chamada `Recruiting11`.  
  
```sql  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)   
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)   
 [Criar um procedimento armazenado](../stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](modify-a-stored-procedure.md)   
 [Excluir um procedimento armazenado](../stored-procedures/delete-a-stored-procedure.md)   
 [Renomear um procedimento armazenado](rename-a-stored-procedure.md)  
  
  
