---
title: ALTER VIEW (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs: TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
ms.assetid: 03eba220-13e2-49e3-bd9d-ea9df84dc28c
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 79d889411d7e974a6ddabd6a753b45f332f1f62a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-view-transact-sql"></a>ALTER VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica uma exibição criada anteriormente. Isto inclui uma exibição indexada. ALTER VIEW não afeta disparadores ou procedimentos armazenados dependentes e não altera permissões.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER VIEW [ schema_name . ] view_name [ ( column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ] [ ; ]  
  
<view_attribute> ::=   
{   
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual a exibição pertence.  
  
 *view_name*  
 É a exibição a ser alterada.  
  
 *coluna*  
 É o nome de uma ou mais colunas, separadas por vírgulas, que farão parte da exibição especificada.  
  
> [!IMPORTANT]  
>  As permissões de coluna serão mantidas apenas quando as colunas tiverem o mesmo nome antes e depois que ALTER VIEW for executado.  
  
> [!NOTE]  
>  Nas colunas da exibição, as permissões de um nome de coluna são aplicadas por uma instrução CREATE VIEW ou ALTER VIEW, independentemente da fonte dos dados subjacentes. Por exemplo, se as permissões são concedidas no **SalesOrderID** coluna em uma instrução CREATE VIEW, uma instrução ALTER VIEW poderá renomear o **SalesOrderID** coluna, como **OrderRef**e ainda terá as permissões associadas à exibição usando **SalesOrderID**.  
  
 ENCRYPTION  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Criptografa as entradas em [sys. syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) que contêm o texto da instrução ALTER VIEW. O uso de WITH ENCRYPTION impede que a exibição seja publicada como parte da replicação do SQL Server.  
  
 SCHEMABINDING  
 Associa a exibição ao esquema da tabela ou tabelas subjacentes. Quando SCHEMABINDING for especificado, as tabelas base não poderão ser modificadas de um modo que possa afetar a definição da exibição. A própria definição da exibição deve primeiramente ser modificada ou descartada a fim de remover dependências na tabela a ser modificada. Quando você usar SCHEMABINDING, o *select_statement* deve incluir os nomes de duas partes (*esquema***.** *objeto*) de tabelas, exibições ou funções definidas pelo usuário que são referenciadas. Todos os objetos referenciados devem estar no mesmo banco de dados.  
  
 As exibições ou tabelas que participam de uma exibição, criadas com a cláusula SCHEMABINDING não podem ser descartadas, a menos que a exibição seja descartada ou alterada, de tal forma que não mais tenha associação de esquema. Caso contrário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro. Além disso, haverá falha na execução de instruções ALTER TABLE nas tabelas que participam de exibições com associação de esquema se essas instruções afetarem a definição da exibição.  
  
 VIEW_METADATA  
 Especifica que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará às APIs DB-Library, ODBC e OLE DB as informações de metadados sobre a exibição, em vez da tabela ou tabelas base, quando metadados do modo de procura forem solicitados para uma consulta que faz referência à exibição. Metadados do modo de procura são metadados adicionais que a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] retorna às APIS do DB-Library, ODBC e OLE DB do lado do cliente. Esses metadados permitem que as APIs do lado do cliente implementem cursores atualizáveis do lado do cliente. Os metadados do modo de procura incluem informações sobre a tabela base às quais as colunas do conjunto de resultados pertencem.  
  
 Para exibições criadas com VIEW_METADATA, os metadados do modo de procura retornam o nome da exibição e não os nomes de tabela base quando descreverem colunas da exibição no conjunto de resultados.  
  
 Quando uma exibição é criada com WITH VIEW_METADATA, todas as suas colunas, exceto um **timestamp** coluna, serão atualizáveis se a exibição tiver INSERT ou UPDATE INSTEAD OF dispara. Para obter mais informações, consulte a seção comentários no [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 AS  
 São as ações que a exibição deve efetuar.  
  
 *select_statement*  
 É a instrução SELECT que define a exibição.  
  
 WITH CHECK OPTION  
 Força todas as instruções de modificação de dados que são executadas em relação à exibição sigam os conjunto de critérios de *select_statement*.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre ALTER VIEW, consulte comentários em [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
> [!NOTE]  
>  Se a definição da exibição anterior foi criada com WITH ENCRYPTION ou CHECK OPTION, essas opções estarão habilitadas apenas se foram incluídas em ALTER VIEW.  
  
 Se uma exibição usada atualmente for modificada com ALTER VIEW, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] obterá um bloqueio de esquema exclusivo na exibição. Quando o bloqueio for concedido e não houver usuários ativos da exibição, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] excluirá todas as cópias da exibição do cache de procedimento. Os planos existentes que façam referência à exibição permanecerão no cache, mas serão recompilados quando invocados.  
  
 ALTER VIEW pode ser aplicado a exibições indexadas; entretanto, ALTER VIEW descarta incondicionalmente todos os índices da exibição.  
  
## <a name="permissions"></a>Permissões  
 Para executar ALTER VIEW, é necessária, no mínimo, permissão ALTER em OBJECT.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma exibição que contém todos os funcionários e suas datas de contratação, denominadas `EmployeeHireDate`. São concedidas permissões para a exibição, mas os requisitos serão alterados para selecionar funcionários cujas datas de contratação sejam anteriores a uma determinada data. Então, `ALTER VIEW` é usado para substituir a exibição.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
 A exibição deve ser alterada para incluir apenas os funcionários que foram contratados antes de `2002`. Se ALTER VIEW não for usado, mas em vez disso a exibição for descartada e recriada, a instrução GRANT usada anteriormente e quaisquer outras instruções que lidem com permissões pertencentes a essa exibição deverão ser inseridas novamente.  
  
```  
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
