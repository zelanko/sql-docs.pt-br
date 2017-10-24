---
title: SET ANSI_WARNINGS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_WARNINGS
- ANSI_WARNINGS_TSQL
- ANSI_WARNINGS
- SET_ANSI_WARNINGS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], ISO standard behavior
- warnings [SQL Server]
- SET ANSI_WARNINGS statement
- ANSI_WARNINGS option
ms.assetid: f82aaab0-334f-427b-89b0-de4af596b4fa
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feee804808cb9ba8d6e3dd97fb512a3a73301e17
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o comportamento padrão ISO para várias condições de erro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ANSI_WARNINGS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_WARNINGS ON;  
```  
  
## <a name="remarks"></a>Comentários  
 SET ANSI_WARNINGS afeta as seguintes condições:  
  
-   Quando definida como ON, se forem exibidos valores nulos em funções de agregação, como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT, será gerada uma mensagem de aviso. Quando definido como OFF, nenhum aviso é emitido.  
  
-   Quando definida como ON, os erros de estouro aritmético e de divisão por zero fazem a instrução ser retornada e uma mensagem de erro é gerada. Quando definida como OFF, os erros de estouro aritmético e de divisão por zero fazem com que valores nulos sejam retornados. O comportamento em que um erro de estouro aritmético e de divisão por zero faz com que valores nulos sejam retornados ocorre se uma inserção ou atualização é tentada um **caracteres**, Unicode, ou **binário** coluna na qual o comprimento novo valor excede o tamanho máximo da coluna. Se SET ANSI_WARNINGS é ON, o INSERT ou UPDATE é cancelada conforme especificado pelo padrão ISO. Espaços em branco à direita são ignorados em colunas de caracteres e valores nulos à direita são ignorados em colunas binárias. Quando OFF, os dados são truncados para o tamanho da coluna e a instrução obtém êxito.  
  
    > [!NOTE]  
    >  Quando o truncamento ocorre em qualquer conversão para ou do **binário** ou **varbinary** dados, nenhum aviso ou erro são emitidos, independentemente das opções SET.  
  
    > [!NOTE]  
    >  O ANSI_WARNINGS não é cumprido quando os parâmetros passam no procedimento armazenado, em uma função definida pelo usuário ou quando declaram ou definem variáveis em uma instrução de lote. Por exemplo, se a variável é definida como **caractere (3)**e definido como um valor maior do que três caracteres, os dados são truncados para o tamanho definido e a inserção ou atualização instrução tem sucesso.  
  
 É possível usar a opção user options desp_configure para definir a configuração padrão para ANSI_WARNINGS em todas as conexões com o servidor. Para obter mais informações, consulte [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 SET ANSI_WARNINGS também deve ser ON quando você estiver criando ou manipulando índices em colunas computadas ou exibições indexadas. Se SET ANSI_WARNINGS for OFF, as instruções CREATE, UPDATE, INSERT e DELETE nas tabelas com índices em colunas computadas ou exibições indexadas falharão. Para obter mais informações sobre as configurações de opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre quando você uso das instruções SET" em [instruções SET &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a opção de banco de dados ANSI_WARNINGS. Ela é equivalente a SET ANSI_WARNINGS. Quando SET ANSI_WARNINGS é ON, são gerados erros ou avisos em erros de divisão por zero, erros de cadeia de caracteres muito longa para a coluna de banco de dados e outros erros semelhantes. Quando SET ANSI_WARNINGS é OFF, esses erros e avisos não estão gerados. O valor padrão no banco de dados modelo para SET ANSI_WARNINGS é OFF. Se não for especificado, a configuração ANSI_WARNINGS será aplicada. Se SET ANSI_WARNINGS for OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o valor da coluna is_ansi_warnings_on no [sys. Databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
 SET ANSI_WARNINGS deve ser definido como ON para executar consultas distribuídas.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_WARNINGS como ON ao conectar-se. Isso pode ser configurado em fontes de dados ODBC, em atributos de conexão ODBC, definidas no aplicativo antes de conectar. O padrão para SET ANSI_WARNINGS é OFF para conexões de aplicativos DB-Library.  
  
 Quando SET ANSI_DEFAULTS é ON, SET ANSI_WARNINGS está habilitado.  
  
 A configuração de SET ANSI_WARNINGS é definida no momento da execução e não no momento da análise.  
  
 Se SET ARITHABORT ou SET ARITHIGNORE estiver definida como OFF e SET ANSI_WARNINGS como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda retornará uma mensagem de erro quando encontrar erros de divisão por zero ou de estouro.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra as três situações previamente mencionadas, com SET ANSI_WARNINGS definido como ON e OFF.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE T1   
(  
   a int,   
   b int NULL,   
   c varchar(20)  
);  
GO  
  
SET NOCOUNT ON;  
  
INSERT INTO T1   
VALUES (1, NULL, '')   
      ,(1, 0, '')  
      ,(2, 1, '')  
      ,(2, 2, '');  
  
SET NOCOUNT OFF;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS ON';  
GO  
  
SET ANSI_WARNINGS ON;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (3, 3, 'Text string longer than 20 characters');  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS OFF';  
GO  
SET ANSI_WARNINGS OFF;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (4, 4, 'Text string longer than 20 characters');  
GO  
SELECT a, b, c   
FROM T1  
WHERE a = 4;  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
DROP TABLE T1  
```  
  
## <a name="see-also"></a>Consulte também  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

