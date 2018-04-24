---
title: ALTER PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_PROCEDURE_TSQL
- ALTER_PROC_TSQL
- ALTER PROC
- ALTER PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROCEDURE statement
- stored procedure modifications [SQL Server]
- modifying stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: ed9b2f76-11ec-498d-a95e-75b490a75733
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c07ffc325c78302ac3cc2098f37dc7cf07a5add4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="alter-procedure-transact-sql"></a>ALTER PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Modifica um procedimento criado anteriormente com a execução da instrução CREATE PROCEDURE no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe do Transact-SQL (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ VARYING ] [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Syntax for SQL Server CLR Stored Procedure  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameterdata_type } [= ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [ ; ] [ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 O nome do esquema ao qual o procedimento pertence.  
  
 *procedure_name*  
 O nome do procedimento a ser alterado. Os nomes de procedimento devem estar de acordo com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 **;** *number*  
 Um inteiro opcional existente que é usado para agrupar procedimentos do mesmo nome, para que possam ser descartados juntos usando uma instrução DROP PROCEDURE.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 **@** *parâmetro*  
 Um parâmetro no procedimento. Podem ser especificados até 2.100 parâmetros.  
  
 [ *type_schema_name***.** ] *data_type*  
 É o tipo de dados do parâmetro e o esquema ao qual ele pertence.  
  
 Para obter informações sobre restrições de tipo de dados, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 VARYING  
 Especifica o conjunto de resultados com suporte como um parâmetro de saída. Este parâmetro é construído dinamicamente pelo procedimento armazenado, e seu conteúdo pode variar. Aplica-se apenas a parâmetros de cursor. Esta opção não é válida para procedimentos CLR.  
  
 *default*  
 É um valor padrão para o parâmetro.  
  
 OUT | OUTPUT  
 Indica que o parâmetro é um parâmetro de retorno.  
  
 READONLY  
 Indica que o parâmetro não pode ser atualizado nem modificado dentro do corpo do procedimento. Se o tipo de parâmetro for um tipo com valor de tabela, deverá ser especificado READONLY.  
  
 RECOMPILE  
 Indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não armazena em cache um plano para esse procedimento e o procedimento é recompilado em tempo de execução.  
  
 ENCRYPTION  
 **Aplica-se a**: SQL Server (de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 Indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] converterá o texto original da instrução ALTER PROCEDURE em um formato ofuscado. A saída do ofuscamento não é diretamente visível em quaisquer exibições de catálogo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários que não tiverem nenhum acesso a tabelas do sistema ou arquivos de banco de dados não poderão recuperar o texto ofuscado. Entretanto, o texto estará disponível para usuários privilegiados que podem acessar as tabelas do sistema na [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) ou acessar diretamente os arquivos do banco de dados. Além disso, os usuários que podem anexar um depurador ao processo de servidor também podem recuperar o procedimento original da memória em tempo de execução. Para obter mais informações sobre como acessar metadados do sistema, consulte [Configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Procedimentos criados com esta opção não podem ser publicados como parte de replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta opção não pode ser especificada para procedimentos armazenados CLR (Common Language Runtime).  
  
> [!NOTE]  
>  Durante um upgrade, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa os comentários ofuscados armazenados em **sys.sql_modules** para recriar procedimentos.  
  
 EXECUTE AS  
 Especifica o contexto de segurança sob o qual o procedimento armazenado é executado depois de ser acessado.  
  
 Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 FOR REPLICATION  

  
 Especifica que procedimentos armazenados que são criados para replicação não podem ser executados no Assinante. Um procedimento armazenado criado com a opção FOR REPLICATION é usado como um filtro de procedimento armazenado e é executado somente durante a replicação. Os parâmetros não poderão ser declarados se FOR REPLICATION for especificado. Esta opção não é válida para procedimentos CLR. A opção RECOMPILE é ignorada para procedimentos criados com FOR REPLICATION.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 { [ BEGIN ] *sql_statement* [;] [ ...*n* ] [ END ] }  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que abrangem o corpo do procedimento. Você pode usar as palavras-chave BEGIN e END para delimitar as instruções. Para obter mais informações, veja as seções Práticas recomendadas, Comentários gerais e Limitações e restrições em [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 EXTERNAL NAME *assembly_name ***.*** class_name ***.*** method_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o método de um assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para um procedimento armazenado CLR a ser referenciado. *classe_name* deve ser um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve existir como uma classe no assembly. Se a classe tiver um nome qualificado de namespace que use um ponto (**.**) para separar partes do namespace, o nome de classe deverá ser delimitado usando colchetes (**[]**) ou aspas (**""**). O método especificado deve ser um método estático da classe.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode executar código CLR. Você pode criar, modificar e remover objetos de banco de dados que referenciam módulos do Common Language Runtime; entretanto, não pode executar essas referências no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até habilitar a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar a opção, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Não há suporte para procedimentos CLR em um banco de dados independente.  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] não podem ser modificados para serem procedimentos armazenados CLR e vice-versa.  
  
 ALTER PROCEDURE não altera permissões e não afeta nenhum procedimento armazenado dependente ou gatilhos. Entretanto, as configurações da sessão atual para QUOTED_IDENTIFIER e ANSI_NULLS são incluídas no procedimento armazenado quando ele é modificado. Se as configurações forem diferentes das que estavam em vigor quando o procedimento armazenado foi originalmente criado, o comportamento do procedimento armazenado poderá mudar.  
  
 Se a definição de procedimento anterior foi criada com WITH ENCRYPTION ou WITH RECOMPILE, essas opções estarão habilitadas somente se tiverem sido incluídas em ALTER PROCEDURE.  
  
 Para obter mais informações sobre procedimentos armazenados, veja [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER** no procedimento, ou requer a associação na função de banco de dados fixa **db_ddladmin**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria o procedimento armazenado `uspVendorAllInfo`. Esse procedimento retorna os nomes de todos os fornecedores que oferecem [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)], os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade. Depois de ser criado, este procedimento é modificado para retornar um conjunto de resultados diferente.  
  
```  
  
IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE Purchasing.uspVendorAllInfo;  
GO  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 O exemplo a seguir altera o procedimento armazenado `uspVendorAllInfo`. Ele remove a cláusula EXECUTE AS CALLER e modifica o corpo do procedimento para retornar apenas os fornecedores que oferecem o produto especificado. As funções `LEFT` e `CASE` personalizam a aparência do conjunto de resultados.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER PROCEDURE Purchasing.uspVendorAllInfo  
    @Product varchar(25)   
AS  
    SET NOCOUNT ON;  
    SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
    'Rating' = CASE v.CreditRating   
        WHEN 1 THEN 'Superior'  
        WHEN 2 THEN 'Excellent'  
        WHEN 3 THEN 'Above average'  
        WHEN 4 THEN 'Average'  
        WHEN 5 THEN 'Below average'  
        ELSE 'No rating'  
        END  
    , Availability = CASE v.ActiveFlag  
        WHEN 1 THEN 'Yes'  
        ELSE 'No'  
        END  
    FROM Purchasing.Vendor AS v   
    INNER JOIN Purchasing.ProductVendor AS pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID   
    WHERE p.Name LIKE @Product  
    ORDER BY v.Name ASC;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Vendor               Product name  Rating    Availability  
-------------------- ------------- -------   ------------  
Proseware, Inc.      LL Crankarm   Average   No  
Vision Cycles, Inc.  LL Crankarm   Superior  Yes  
(2 row(s) affected)`  
```  

## <a name="see-also"></a>Consulte Também  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)  
  
  
