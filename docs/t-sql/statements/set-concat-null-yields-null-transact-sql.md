---
title: SET CONCAT_NULL_YIELDS_NULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cdaa57594049ca9c7bd088120ae119ec7c58c151
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041837"
---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Controla se os resultados de concatenação serão tratados como valores de cadeia de caracteres nulos ou vazios.  
  
> [!IMPORTANT]  
>  Em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL sempre estará ON e quaisquer aplicativos que definam explicitamente a opção como OFF gerarão um erro. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>Remarks  
 Quando SET CONCAT_NULL_YIELDS_NULL for ON, a concatenação de um valor nulo com uma cadeia de caracteres gera um resultado NULL. Por exemplo, `SELECT 'abc' + NULL` gera `NULL`. Quando SET CONCAT_NULL_YIELDS_NULL for OFF, a concatenação de um valor nulo com uma cadeia de caracteres gera a própria cadeia de caracteres (o valor nulo é tratado como uma cadeia de caracteres vazia). Por exemplo, `SELECT 'abc' + NULL` gera `abc`.  
  
 Se SET CONCAT_NULL_YIELDS_NULL não for especificado, a configuração da opção de banco de dados **CONCAT_NULL_YIELDS_NULL** será aplicada.  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL é a mesma configuração CONCAT_NULL_YIELDS_NULL de ALTER DATABASE.  
  
 A configuração de SET CONCAT_NULL_YIELDS_NULL é definida na execução ou em tempo de execução, e não no momento da análise.  

SET CONCAT_NULL_YIELDS_NULL deve estar como **ON** quando você criar ou alterar índices em colunas computadas, exibições indexadas ou índices espaciais. Se SET CONCAT_NULL_YIELDS_NULL estiver como **OFF**, haverá falha em todas as instruções CREATE, UPDATE, INSERT e DELETE nas tabelas com índices em colunas computadas, exibições indexadas ou índices espaciais. Para obter mais informações sobre as configurações da opção SET com exibições indexadas e índices em colunas computadas, consulte "Considerações sobre o uso das instruções SET" em [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md).
  
 Quando CONCAT_NULL_YIELDS_NULL é definido como OFF, a concatenação de cadeia de caracteres entre limites de servidor não acontece.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @CONCAT_NULL_YIELDS_NULL VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_NULL_YIELDS_NULL = 'ON';  
SELECT @CONCAT_NULL_YIELDS_NULL AS CONCAT_NULL_YIELDS_NULL;  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso das duas configurações `SET CONCAT_NULL_YIELDS_NULL`.  
  
```  
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
