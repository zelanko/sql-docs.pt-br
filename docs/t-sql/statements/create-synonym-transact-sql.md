---
title: CREATE SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SYNONYM_TSQL
- SYNONYM_TSQL
- SYNONYM
- CREATE SYNONYM
dev_langs:
- TSQL
helpviewer_keywords:
- alternate names [SQL Server]
- names [SQL Server], synonyms
- CREATE SYNONYM statement
- synonyms [SQL Server], creating
ms.assetid: 41313809-e970-449c-bc35-85da2ef96e48
caps.latest.revision: 43
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9be0a9961e83896303eade9dfb68696cec7af31c
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785820"
---
# <a name="create-synonym-transact-sql"></a>CREATE SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um novo sinônimo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
  
CREATE SYNONYM [ schema_name_1. ] synonym_name FOR <object>  
  
<object> :: =  
{  
    [ server_name.[ database_name ] . [ schema_name_2 ]. object_name   
  | database_name . [ schema_name_2 ].| schema_name_2. ] object_name  
}  
```  
  
```  
-- Azure SQL Database Syntax  
  
CREATE SYNONYM [ schema_name_1. ] synonym_name FOR < object >  
  
< object > :: =  
{  
    [database_name. [ schema_name_2 ].| schema_name_2. ] object_name  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name_1*  
 Especifica o esquema no qual o sinônimo é criado. Se *schema* não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o esquema padrão do usuário atual.  
  
 *synonym_name*  
 É o nome do novo sinônimo.  
  
 *server_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É o nome do servidor no qual o objeto base está localizado.  
  
 *database_name*  
 É o nome do banco de dados no qual o objeto base está localizado. Se *database_name* não for especificado, o nome do banco de dados atual será usado.  
  
 *schema_name_2*  
 É o nome do esquema do objeto base. Se *schema_name* não for especificado, o esquema padrão do usuário atual será usado.  
  
 *object_name*  
 É o nome do objeto base que o sinônimo referencia.  
  
 O Banco de Dados SQL do Windows Azure oferece suporte ao formato de nome de três partes database_name.[schema_name].object_name quando o database_name é o banco de dados atual ou o database_name é tempdb e o object_name começa com #.  
  
## <a name="remarks"></a>Remarks  
 O objeto base não precisa existir no momento da criação do sinônimo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica a existência do objeto base em tempo de execução.  
  
 Podem ser criados sinônimos para os seguintes tipos de objetos:  
  
|||  
|-|-|  
|Procedimento armazenado de assembly (CLR)|Função com valor de tabela de assembly (CLR)|  
|Função escalar de assembly (CLR)|Funções de agregação de assembly (CLR)|  
|Procedimento de filtro de replicação|Procedimento armazenado estendido|  
|Função escalar SQL|Função com valor de tabela SQL|  
|Função com valor de tabela embutida SQL|Procedimento armazenado SQL|  
|Exibição|Tabela<sup>1</sup> (definida pelo usuário)|  
  
 <sup>1 Inclui tabelas temporárias locais e globais</sup>  
  
 Não há suporte para nomes de quatro partes para objetos base de função.  
  
 É possível criar, descartar e referenciar sinônimos em SQL dinâmico.  
  
## <a name="permissions"></a>Permissões  
 Para criar um sinônimo em um determinado esquema, o usuário deve ter a permissão CREATE SYNONYM e ou ser proprietário do esquema ou ter a permissão ALTER SCHEMA.  
  
 A permissão CREATE SYNONYM pode ser concedida.  
  
> [!NOTE]  
>  Você não precisa de permissão no objeto base para compilar a instrução CREATE SYNONYM, pois toda a verificação de permissão no objeto base é adiada até o tempo de execução.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-synonym-for-a-local-object"></a>A. Criando um sinônimo para um objeto local  
 O exemplo a seguir cria primeiro um sinônimo para o objeto base, `Product`, no banco de dados `AdventureWorks2012` e, em seguida, consulta o sinônimo.  
  
```  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
  
-- Query the Product table by using the synonym.  
SELECT ProductID, Name   
FROM MyProduct  
WHERE ProductID < 5;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------------- 
 ProductID   Name 
 ----------- -------------------------- 
 1           Adjustable Race 
 2           Bearing Ball 
 3           BB Ball Bearing 
 4           Headset Ball Bearings 

 (4 row(s) affected)
``` 
  
### <a name="b-creating-a-synonym-to-remote-object"></a>B. Criando um sinônimo para objeto remoto  
 No exemplo a seguir, o objeto base, `Contact`, reside em um servidor remoto denominado `Server_Remote`.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
EXEC sp_addlinkedserver Server_Remote;  
GO  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee FOR Server_Remote.AdventureWorks2012.HumanResources.Employee;  
GO  
```  
  
### <a name="c-creating-a-synonym-for-a-user-defined-function"></a>C. Criando um sinônimo para uma função definida pelo usuário  
 O exemplo a seguir cria uma função chamada `dbo.OrderDozen` que aumenta o pedido para uma quantidade regular de doze unidades. Em seguida, o exemplo cria o sinônimo `dbo.CorrectOrder` para a função `dbo.OrderDozen`.  
  
```  
-- Creating the dbo.OrderDozen function  
CREATE FUNCTION dbo.OrderDozen (@OrderAmt int)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
IF @OrderAmt % 12 <> 0  
BEGIN  
    SET @OrderAmt +=  12 - (@OrderAmt % 12)  
END  
RETURN(@OrderAmt);  
END;  
GO  
  
-- Using the dbo.OrderDozen function  
DECLARE @Amt int;  
SET @Amt = 15;  
SELECT @Amt AS OriginalOrder, dbo.OrderDozen(@Amt) AS ModifiedOrder;  
  
-- Create a synonym dbo.CorrectOrder for the dbo.OrderDozen function.  
CREATE SYNONYM dbo.CorrectOrder  
FOR dbo.OrderDozen;  
GO  
  
-- Using the dbo.CorrectOrder synonym.  
DECLARE @Amt int;  
SET @Amt = 15;  
SELECT @Amt AS OriginalOrder, dbo.CorrectOrder(@Amt) AS ModifiedOrder;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DROP SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
