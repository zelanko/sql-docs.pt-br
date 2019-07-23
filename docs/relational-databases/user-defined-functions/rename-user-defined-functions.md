---
title: Renomear funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 274c79dabe90098094423b2994edb93603e649e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123570"
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
  
  
