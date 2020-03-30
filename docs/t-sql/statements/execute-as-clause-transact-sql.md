---
title: Cláusula EXECUTE AS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2dfba9eef86ab77ec114bc74712d9573fb5e4c48
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70155055"
---
# <a name="execute-as-clause-transact-sql"></a>Cláusula EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível definir o contexto de execução dos seguintes módulos definidos pelo usuário: funções (exceto com valor de tabela embutida), procedimentos, filas e gatilhos.  
  
 Especificando o contexto no qual o módulo é executado, você pode controlar qual conta de usuário o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa para validar permissões em objetos referenciados pelo módulo. Isso dá mais flexibilidade e controle no gerenciamento de permissões na cadeia de objetos existente entre os módulos definidos pelo usuário e os objetos referenciados por esses módulos. A permissões devem ser concedidas a usuários somente no próprio módulo, sem necessitar conceder permissões explícitas nos objetos referenciados. Somente o usuário que o módulo está representando tem permissões nos objetos acessados pelo módulo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 **CALLER**  
 Especifica que as instruções do módulo são executadas no contexto do chamador do módulo. O usuário executando o módulo deve ter permissões apropriadas não apenas no módulo em si, mas também em qualquer objeto que seja referenciado pelo módulo.  
  
 CALLER é o padrão para todos os módulos, exceto filas, e tem o mesmo comportamento que no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 CALLER não pode ser especificado em uma instrução CREATE QUEUE ou ALTER QUEUE.  
  
 **SELF**  
 EXECUTE AS SELF equivale a EXECUTE AS *user_name*, em que o usuário especificado é a pessoa que cria ou altera o módulo. A ID de usuário real da pessoa que cria ou modifica os módulos é armazenada na coluna **execute_as_principal_id** da exibição do catálogo **sys.sql_modules** ou **sys.service_queues**.  
  
 SELF é o padrão para filas.  
  
> [!NOTE]  
>  Para alterar a ID de usuário de **execute_as_principal_id** da exibição do catálogo **sys.service_queues**, é necessário especificar explicitamente a configuração EXECUTE AS na instrução ALTER QUEUE.  
  
 OWNER  
 Especifica que as instruções do módulo são executadas no contexto do proprietário atual do módulo. Se o módulo não tiver um proprietário especificado, o proprietário do esquema do módulo será usado. OWNER não pode ser especificado para gatilhos DDL ou de logon.  
  
> [!IMPORTANT]  
>  OWNER deve mapear a uma conta singleton e não deve ser uma função ou grupo.  
  
 **'** *user_name* **'**  
 Especifica que as instruções dentro do módulo sejam executadas no contexto do usuário especificado em *user_name*. As permissões de qualquer objeto dentro do módulo são verificadas em relação a *user_name*. *user_name* não pode ser especificado para gatilhos DDL com escopo de servidor ou gatilhos de logon. Use *login_name*.  
  
 *user_name* deve existir no banco de dados atual e deve ser uma conta singleton. *user_name* não pode ser um grupo, uma função, um certificado, uma chave ou conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT AUTHORITY\LocalSystem.  
  
 A ID de usuário do contexto de execução é armazenada em metadados e pode ser exibida na coluna **execute_as_principal_id** da exibição do catálogo **sys.sql_modules** ou **sys.assembly_modules**.  
  
 **'** *login_name* **'**  
 Especifica que as instruções do módulo sejam executadas no contexto do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado em *login_name*. As permissões de qualquer objeto dentro do módulo são verificadas em relação a *login_name*. *login_name* pode ser especificado apenas para gatilhos DDL com escopo de servidor ou gatilhos de logon.  
  
 *login_name* não pode ser um grupo, uma função, um certificado, uma chave ou conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT AUTHORITY\LocalSystem.  
  
## <a name="remarks"></a>Comentários  
 A forma como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] avalia as permissões nos objetos que são referenciados no módulo depende da cadeia de propriedade que existente entre os objetos de chamada e os objetos referenciados. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a cadeia de propriedade era o único método disponível para não ter de conceder ao usuário chamador acesso a todos os objetos referenciados.  
  
 A cadeia de propriedade tem as seguintes limitações:  
  
-   Só se aplica a instruções DML: SELECT, INSERT, UPDATE e DELETE.  
  
-   Os proprietários da chamada e os objetos chamados devem ser os mesmos.  
  
-   Não se aplica a consultas dinâmicas no módulo.  
  
 Independentemente do contexto de execução especificado no módulo, as seguintes ações sempre se aplicam:  
  
-   Quando o módulo é executado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] primeiro verifica se o usuário executando o módulo tem a permissão EXECUTE no módulo.  
  
-   As regras de cadeia de propriedade continuam aplicáveis. Isso significa que, se os proprietários dos objetos chamadores e chamados são os mesmos, nenhuma permissão é verificada nos objetos subjacentes.  
  
 Quando um usuário executa um módulo que foi especificado para ser executado em um contexto diferente de CALLER, a permissão do usuário para executar o módulo é verificada, mas as verificações de permissões adicionais nos objetos que são acessados pelo módulo são executadas na conta de usuário especificada na cláusula EXECUTE AS. O usuário que executa o módulo está, na verdade, representando o usuário especificado.  
  
 O contexto especificado na cláusula EXECUTE AS do módulo é válido somente para a duração da execução do módulo. O contexto é revertido ao chamador quando a execução de módulo é concluída.  
  
## <a name="specifying-a-user-or-login-name"></a>Especificando um nome de logon ou usuário  
 Um usuário de banco de dados ou logon de servidor especificado na cláusula EXECUTE AS de um módulo não pode ser descartado até que o módulo seja modificado para ser executado em outro contexto.  
  
 O nome de usuário ou de logon especificado na cláusula EXECUTE AS deverá existir como uma entidade de segurança em **sys.database_principals** ou **sys.server_principals**, respectivamente, caso contrário, a operação de criação ou alteração do módulo falhará. Além disso, o usuário que cria ou altera o módulo deve ter as permissões IMPERSONATE no principal.  
  
 Se o usuário tiver acesso implícito ao banco de dados ou à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] através de uma associação de grupo do Windows, o usuário especificado na cláusula EXECUTE AS será criado implicitamente quando o modulo for criado, caso um dos seguintes requisitos exista:  
  
-   O usuário ou logon especificado é um membro da função de servidor fixa **sysadmin**.  
  
-   O usuário que está criando o módulo tem permissão para criar os principais.  
  
 Quando nenhum desses requisitos é atendido, a operação de criar o módulo falha.  
  
> [!IMPORTANT]  
>  Se o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) for executado em uma conta local (serviço local ou conta de usuário local), ele não terá privilégios para obter associações de grupo de uma conta de domínio do Windows que for especificada na cláusula EXECUTE AS. Isso fará a execução do módulo falhar.  
  
 Por exemplo, considere as seguintes condições:  
  
-   O grupo **CompanyDomain\SQLUsers** tem acesso ao banco de dados **Sales**.  
  
-   **CompanyDomain\SqlUser1** é membro de **SQLUsers** e, portanto, tem acesso ao banco de dados **Sales**.  
  
-   O usuário que está criando ou está alterando o módulo tem permissões para criar os principais.  
  
 Quando a seguinte instrução `CREATE PROCEDURE` é executada, o `CompanyDomain\SqlUser1` é implicitamente criado como um principal de banco de dados no banco de dados `Sales`.  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>Usando a instrução autônoma EXECUTE AS CALLER  
 Use a instrução autônoma EXECUTE AS CALLER em um módulo ao definir o contexto de execução para o chamador do módulo.  
  
 Suponha que o procedimento armazenado a seguir seja chamado de `SqlUser2`.  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>Usando EXECUTE AS para definir conjuntos de permissões personalizadas  
 Especificar um contexto de execução para um módulo pode ser muito útil quando ao definir conjuntos de permissões personalizadas. Por exemplo, algumas ações, como TRUNCATE TABLE, não têm permissões concessíveis. Incorporando a instrução TRUNCATE TABLE em um módulo e especificando que o módulo execute como um usuário que tem permissões para alterar a tabela, você pode estender as permissões para truncar a tabela para o usuário ao qual fora, concedidas permissões EXECUTE no módulo.  
  
 Para exibir a definição do módulo com o contexto de execução especificado, use a exibição do catálogo [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
## <a name="best-practice"></a>Melhor prática  
 Especifica um logon ou usuário com os privilégios mínimos exigidos para executar as operações definidos no módulo. Por exemplo, não especifique uma conta de proprietário de banco de dados a menos que essas permissões sejam necessárias.  
  
## <a name="permissions"></a>Permissões  
 Para executar um módulo especificado com EXECUTE AS, o chamador precisar ter permissões EXECUTE no módulo.  
  
 Para executar um módulo CLR especificado com EXECUTE AS que acesse recursos em outro banco de dados ou servidor, o banco de dados ou servidor de destino deve confiar no autenticador do banco de dados do qual o módulo origina (o banco de dados de origem).  
  
 Para especificar a cláusula EXECUTE AS ao criar ou modificar um módulo, é necessário ter as permissões IMPERSONATE no principal especificado e também permissões para criar o módulo. Você sempre pode se representar. Quando nenhum contexto de execução é especificado ou EXECUTE AS CALLER é especificado, as permissões de IMPERSONATE não são obrigatórias.  
  
 Para especificar um *login_name* ou *user_name* que tem acesso implícito ao banco de dados por meio de uma associação a um grupo do Windows, é necessário ter permissões CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um procedimento armazenado no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e atribui o contexto de execução a `OWNER`.  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.service_queues &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
