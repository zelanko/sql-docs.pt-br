---
title: PRINT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51377ebe291fe4c76d8761aaba74eab8f5201108
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="print-transact-sql"></a>IMPRESSÃO-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma mensagem definida pelo usuário ao cliente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  

PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_str*  
 É uma cadeia de caracteres ou uma constante de cadeia de caracteres Unicode. Para obter mais informações, consulte [constantes &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***local_variable*  
 É uma variável de qualquer tipo de dados de caractere válido. **@***local_variable* devem ser **char**, **nchar**, **varchar**, ou **nvarchar**, ou deve ser capaz de ser implicitamente convertido para esses tipos de dados.  
  
 *string_expr*  
 É uma expressão que retorna uma cadeia de caracteres. Pode incluir valores literais, funções e variáveis concatenadas. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Uma cadeia de caracteres de mensagem pode ter até 8.000 caracteres se for uma cadeia de caracteres não Unicode e 4.000 caracteres se for uma cadeia de caracteres Unicode. Cadeias de caracteres mais longas são truncadas. O **varchar (max)** e **nvarchar (max)** tipos de dados são truncados para tipos de dados que são maiores do que **varchar(8000)** e **nvarchar (4000)**.  
  
 RAISERROR também pode ser usado para retornar mensagens. RAISERROR tem estas vantagens sobre PRINT:  
  
-   RAISERROR oferece suporte à substituição de argumentos em uma cadeia de caracteres de mensagem de erro usando um mecanismo modelado sobre a função printf da biblioteca padrão da linguagem C.  
  
-   RAISERROR pode especificar um número de erro exclusivo, uma severidade e um código de estado, além da mensagem de texto.  
  
-   RAISERROR pode ser usado para retornar mensagens definidas pelo usuário criadas com o uso do procedimento armazenado do sistema sp_addmessage.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. Executando print condicionalmente (IF EXISTS)  
 O exemplo a seguir usa a instrução `PRINT` para retornar uma mensagem condicionalmente.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. Construindo e exibindo uma cadeia de caracteres  
 O exemplo a seguir converte os resultados da função `GETDATE` em um tipo de dados `nvarchar` e o concatena com o texto literal a ser retornado por `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. Executando print condicionalmente  
 O exemplo a seguir usa a instrução `PRINT` para retornar uma mensagem condicionalmente.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
### <a name="d-building-and-displaying-a-string"></a>D. Construindo e exibindo uma cadeia de caracteres  
 O exemplo a seguir converte os resultados da função `GETDATE` em um tipo de dados `nvarchar` e o concatena com o texto literal a ser retornado por `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  


