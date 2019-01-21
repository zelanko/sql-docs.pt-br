---
title: SET ANSI_WARNINGS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: af30fd34d42b296e9b83bbd537dcff411cd42608
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143246"
---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o comportamento padrão ISO para várias condições de erro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ANSI_WARNINGS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_WARNINGS ON
```

## <a name="remarks"></a>Remarks  
 SET ANSI_WARNINGS afeta as seguintes condições:  
  
-   Quando definida como ON, se forem exibidos valores nulos em funções de agregação, como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT, será gerada uma mensagem de aviso. Quando definido como OFF, nenhum aviso é emitido.  
  
-   Quando definida como ON, os erros de estouro aritmético e de divisão por zero fazem a instrução ser retornada e uma mensagem de erro é gerada. Quando definida como OFF, os erros de estouro aritmético e de divisão por zero fazem com que valores nulos sejam retornados. O comportamento em que um erro de estouro aritmético e ou divisão por zero faz valores nulos serem retornados ocorrerá se houver uma tentativa de INSERT ou UPDATE em uma coluna **character**, Unicode ou **binary** na qual a extensão do novo valor exceda o tamanho máximo da coluna. Se SET ANSI_WARNINGS está ON, INSERT ou UPDATE é cancelada, como especificado pelo padrão ISO. Espaços em branco à direita são ignorados em colunas de caracteres e valores nulos à direita são ignorados em colunas binárias. Quando OFF, os dados são truncados para o tamanho da coluna e a instrução obtém êxito.  
  
> [!NOTE]  
> Quando o truncamento ocorre em qualquer conversão de ou para dados **binary** ou **varbinary**, nenhum aviso ou erro é emitido, independentemente das opções SET.  
  
> [!NOTE]  
> O ANSI_WARNINGS não é cumprido quando os parâmetros passam no procedimento armazenado, em uma função definida pelo usuário ou quando declaram ou definem variáveis em uma instrução de lote. Por exemplo, se a variável for definida como **char(3)** e, em seguida, configurada com um valor maior que três caracteres, os dados serão truncados até o tamanho definido e a instrução INSERT ou UPDATE terá êxito.  
  
É possível usar a opção user options desp_configure para definir a configuração padrão para ANSI_WARNINGS em todas as conexões com o servidor. Para obter mais informações, consulte [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
ANSI_WARNINGS também deve ser ON quando você estiver criando ou manipulando índices em colunas computadas ou exibições indexadas. Se SET ANSI_WARNINGS for OFF, as instruções CREATE, UPDATE, INSERT e DELETE nas tabelas com índices em colunas computadas ou exibições indexadas falharão. Para obter mais informações sobre as configurações da opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre o uso das instruções SET" em [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a opção de banco de dados ANSI_WARNINGS. Ela é equivalente a SET ANSI_WARNINGS. Quando SET ANSI_WARNINGS é ON, são gerados erros ou avisos em erros de divisão por zero, erros de cadeia de caracteres muito longa para a coluna de banco de dados e outros erros semelhantes. Quando SET ANSI_WARNINGS é OFF, esses erros e avisos não estão gerados. O valor padrão no banco de dados modelo para SET ANSI_WARNINGS é OFF. Se não for especificado, a configuração ANSI_WARNINGS será aplicada. Se SET ANSI_WARNINGS for OFF, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará o valor da coluna is_ansi_warnings_on na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
> [!IMPORTANT]
> SET ANSI_WARNINGS deve ser definido como ON para executar consultas distribuídas.  
  
 O driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC e o Provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_WARNINGS como ON ao conectar. Isso pode ser configurado em fontes de dados ODBC, em atributos de conexão ODBC, definidas no aplicativo antes de conectar. O padrão para SET ANSI_WARNINGS é OFF para conexões de aplicativos DB-Library.  
  
Quando ANSI_DEFAULTS é ON, ANSI_WARNINGS está habilitado.  
  
A configuração de ANSI_WARNINGS é definida no momento da execução, e não no momento da análise.  
  
Se SET ARITHABORT ou SET ARITHIGNORE estiver definida como OFF e SET ANSI_WARNINGS como ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda retornará uma mensagem de erro quando encontrar erros de divisão por zero ou de estouro.  
  
Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```sql  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Permissões  
Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir demonstra as três situações previamente mencionadas, com SET ANSI_WARNINGS definido como ON e OFF.  
  
```sql  
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
```

Agora defina ANSI_WARNINGS como ON e teste.

```sql
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
```

Agora defina ANSI_WARNINGS como OFF e teste.

```sql
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
  
DROP TABLE T1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
