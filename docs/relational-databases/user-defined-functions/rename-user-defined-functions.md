---
title: Renomear funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: udf
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc1db3ef29e072edda79e31af4372ce8796a017e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="rename-user-defined-functions"></a>Renomear funções definidas pelo usuário
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Você pode renomear funções definidas pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear funções definidas pelo usuário utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os nomes de funções devem ser compatíveis com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
-   Renomear uma função definida pelo usuário não alterará o nome do objeto correspondente na coluna de definição da exibição de catálogo **sys.sql_modules** . Assim, é recomendável não renomear esse tipo de objeto. Em vez disso, remova-o e recrie o procedimento armazenado com seu nome novo.  
  
-   A alteração do nome ou definição de uma função definida pelo usuário pode causar falha em objetos dependentes que não são atualizados para refletir as alterações que tenham sido feitas na função.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para remover a função, é necessário ter a permissão ALTER no esquema ao qual pertence a função ou a permissão CONTROL na função. Para recriar a função, é necessário ter a permissão CREATE FUNCTION no banco de dados e a permissão ALTER no esquema no qual a função está sendo criada.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-user-defined-functions"></a>Para renomear funções definidas pelo usuário  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição ao lado do banco de dados que contém a função que você deseja renomear e  
  
2.  Clique no sinal de adição ao lado da pasta **Programação** .  
  
3.  Clique no sinal de mais ao lado da pasta que contém a função que você deseja renomear:  
  
    -   Table-valued Function  
  
    -   Função de valor escalar  
  
    -   Função de agregação  
  
4.  Clique com o botão direito do mouse na função que você deseja renomear e selecione **Renomear**.  
  
5.  Digite o novo nome da função.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para renomear funções definidas pelo usuário**  
  
 Esta tarefa não pode ser executada usando instruções Transact-SQL. Para renomear uma função definida pelo usuário usando Transact-SQL, primeiro você deve excluir a função existente e depois recriá-la com o novo nome. Verifique se todo o código e os aplicativos que usavam o nome antigo da função agora usam o nome novo.  
  
 Para obter mais informações, veja [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) e [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [Exibir funções definidas pelo usuário](../../relational-databases/user-defined-functions/view-user-defined-functions.md)  
  
  
