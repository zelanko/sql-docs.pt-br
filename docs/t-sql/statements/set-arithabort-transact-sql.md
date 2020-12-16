---
description: SET ARITHABORT (Transact-SQL)
title: SET ARITHABORT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f2251603be01262faaf775a654808d7c428a53c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476527"
---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Encerra uma consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

### <a name="syntax-for-ssnoversion-mdmd-and-sssodfull-mdmd"></a>Sintaxe para [!INCLUDE[ssnoversion-md.md](../../includes/ssnoversion-md.md)] e [!INCLUDE[sssodfull-md.md](../../includes/sssodfull-md.md)]
```syntaxsql
SET ARITHABORT { ON | OFF }
```

### <a name="syntax-for-sssdw-mdmd-and-sspdw-mdmd"></a>Sintaxe para [!INCLUDE[sssdw-md.md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md.md](../../includes/sspdw-md.md)]
```syntaxsql
SET ARITHABORT ON
```
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
Sempre defina ARITHABORT como ON nas sessões de logon. A definição de ARITHABORT como OFF pode afetar negativamente a otimização de consulta, levando a problemas de desempenho.  
  
> [!WARNING]  
>  A configuração padrão ARITHABORT de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é ON. Os aplicativos cliente que definem ARITHABORT como OFF podem receber planos de consulta diferentes, dificultando a solução de problemas de consultas executadas insatisfatoriamente. Ou seja, a mesma consulta pode ser executada rapidamente no Management Studio, mas lentamente no aplicativo. Ao solucionar problemas de consultas com [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], sempre faça a correspondência com a configuração ARITHABORT do cliente.  
  
Quando as opções SET ARITHABORT e SET ANSI WARNINGS são definidas como ON, essas condições de erro provocam o encerramento da consulta.  
  
Quando as opções SET ARITHABORT e SET ANSI WARNINGS são definidas como OFF, essas condições de erro provocam o encerramento do lote. Se ocorrer erro em uma transação, a transação será revertida. Quando a opção SET ARITHABORT é definida como OFF e um desses erros ocorre, uma mensagem de aviso aparece e o resultado da operação aritmética é NULL.  
  
Se as opções SET ARITHABORT e SET ANSI WARNINGS estão definidas como OFF e um desses erros ocorre, uma mensagem de aviso é exibida e o resultado da operação aritmética é NULL.  
  
> [!NOTE]  
>  Se nem SET ARITHABORT e nem SET ARITHIGNORE estão definidas como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna NULL e uma mensagem de aviso é exibida após a execução da consulta.  
  
Quando ANSI_WARNINGS tem um valor igual a ON e o nível de compatibilidade do banco de dados é definido como 90 ou superior, ARITHABORT está implicitamente ATIVADO, independentemente da configuração do valor. Se o nível de compatibilidade do banco de dados for definido como 80 ou menos, a opção ARITHABORT deverá ser definida explicitamente como ON.  
  
Na avaliação da expressão, se SET ARITHABORT é OFF e se uma instrução INSERT, UPDATE ou DELETE encontra um erro aritmético, de estouro, de divisão por zero ou de domínio, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insere ou atualiza um valor NULL. Se a coluna de destino não for anulável, a ação de inserção ou atualização falhará e o usuário receberá uma mensagem de erro.  
  
Quando SET ARITHABORT ou SET ARITHIGNORE estiver definida como OFF e SET ANSI_WARNINGS como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda retornará uma mensagem de erro quando encontrar erros de divisão por zero ou de estouro.  
  
Quando a opção SET ARITHABORT for definida como OFF e ocorrer um erro de anulação durante a avaliação da condição booliana de uma instrução IF, o branch FALSE será executado.
  
SET ARITHABORT deve ser ON quando você estiver criando ou alterando índices em colunas computadas ou modos de exibição indexados. Se SET ARITHABORT for OFF, toda instrução CREATE, UPDATE, INSERT e DELETE das tabelas com índices em colunas computadas ou modos de exibição indexados falhará.
  
A configuração de SET ARITHABORT é definida no momento da execução e não no momento da análise.  
  
Para exibir a configuração atual de SET ARITHABORT, execute a seguinte consulta:
  
```sql  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>Permissões  
Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
O exemplo seguinte demonstra erros de divisão por zero e de estouro com as configurações de `SET ARITHABORT`.  
  
```sql  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '**_ SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '_*_ Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '_*_ Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '_*_ Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '_*_ Resulting data - should be no data';  
GO  
SELECT _   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '**_ Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '_*_ Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '_*_ Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '_*_ Resulting data - should be 0 rows';  
GO  
SELECT _   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHIGNORE &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
