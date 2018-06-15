---
title: IDENT_CURRENT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IDENT_CURRENT
- IDENT_CURRENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- last identity value generated for table
- identity values [SQL Server], last generated
- identity columns, current value
- IDENT_CURRENT function
ms.assetid: 21517ced-39f5-4cd8-8d9c-0a0b8aff554a
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8ad92b06aee95a2de975909ad90f3001b92169fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053083"
---
# <a name="identcurrent-transact-sql"></a>IDENT_CURRENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o valor da última identidade gerado para uma tabela ou exibição especificada. O valor da última identidade gerado pode ser para qualquer sessão e para qualquer escopo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IDENT_CURRENT( 'table_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 É o nome da tabela cujo valor de identidade é retornado. *table_name* é **varchar**, sem nenhum padrão.  
  
## <a name="return-types"></a>Tipos de retorno  
 **numeric(38,0)**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas emissoras de metadados, como IDENT_CURRENT, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Remarks  
 IDENT_CURRENT é semelhante às funções de identidade SCOPE_IDENTITY e @@IDENTITY do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. As três funções retornam valores de identidade gerados por último. Entretanto, o escopo e a sessão nas quais o *último* está definido em cada uma dessas funções difere:  
  
-   IDENT_CURRENT retorna o último valor de identidade gerado para uma tabela específica em qualquer sessão e escopo.  
  
-   @@IDENTITY retorna o último valor de identidade gerado para qualquer tabela na sessão atual, em todos os escopos.  
  
-   SCOPE_IDENTITY retorna o último valor de identidade gerado para qualquer tabela na sessão e no escopo atuais.  
  
 Quando o valor IDENT_CURRENT é NULL (porque a tabela nunca teve linhas ou foi truncada), a função IDENT_CURRENT retornar o valor semente.  
  
 Instruções e transações com falha podem alterar a identidade atual de uma tabela e criar lacunas nos valores da coluna de identidade. O valor de identidade nunca é revertido, mesmo que a transação que tentou inserir o valor na tabela não seja confirmada. Por exemplo, se uma instrução INSERT falhar por causa de uma violação IGNORE_DUP_KEY, o valor de identidade atual para a tabela ainda será incrementado.  
  
 Seja cauteloso ao usar IDENT_CURRENT para prever o próximo valor de identidade gerado. O valor gerado real pode ser diferente de IDENT_CURRENT mais IDENT_INCR devido a inserções executadas por outras sessões.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-last-identity-value-generated-for-a-specified-table"></a>A. Retornando o último valor de identidade gerado para uma tabela especificada  
 O exemplo a seguir retorna o último valor de identidade gerado para a tabela `Person.Address` no banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENT_CURRENT ('Person.Address') AS Current_Identity;  
GO  
```  
  
### <a name="b-comparing-identity-values-returned-by-identcurrent-identity-and-scopeidentity"></a>B. Comparando valores de identidade retornados por IDENT_CURRENT, @@IDENTITY e SCOPE_IDENTITY  
 O exemplo a seguir mostra os valores de identidade diferentes que são retornados por `IDENT_CURRENT`, `@@IDENTITY` e `SCOPE_IDENTITY`.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't6', N'U') IS NOT NULL   
    DROP TABLE t6;  
GO  
IF OBJECT_ID(N't7', N'U') IS NOT NULL   
    DROP TABLE t7;  
GO  
CREATE TABLE t6(id int IDENTITY);  
CREATE TABLE t7(id int IDENTITY(100,1));  
GO  
CREATE TRIGGER t6ins ON t6 FOR INSERT   
AS  
BEGIN  
   INSERT t7 DEFAULT VALUES  
END;  
GO  
--End of trigger definition  
  
SELECT id FROM t6;  
--IDs empty.  
  
SELECT id FROM t7;  
--ID is empty.  
  
--Do the following in Session 1  
INSERT t6 DEFAULT VALUES;  
SELECT @@IDENTITY;  
/*Returns the value 100. This was inserted by the trigger.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns the value 1. This was inserted by the   
INSERT statement two statements before this query.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns value inserted into t7, that is in the trigger.*/  
  
SELECT IDENT_CURRENT('t6');  
/* Returns value inserted into t6. This was the INSERT statement four statements before this query.*/  
  
-- Do the following in Session 2.  
SELECT @@IDENTITY;  
/* Returns NULL because there has been no INSERT action   
up to this point in this session.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns NULL because there has been no INSERT action   
up to this point in this scope in this session.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns the last value inserted into t7.*/  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
