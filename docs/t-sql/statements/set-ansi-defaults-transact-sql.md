---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 02353688efb79b4c2dbb7c4bc3d9ed0d4d5e0a37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913938"
---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Controla um grupo de configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que coletivamente especificam algum comportamento padrão ISO.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Sintaxe

```
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>Remarks  
ANSI_DEFAULTS é uma configuração do lado do servidor que o cliente não modifica. O cliente gerencia suas próprias configurações. Por padrão, essas configurações são o oposto da configuração de servidor. Os usuários não devem modificar a configuração de servidor. Para alterar o comportamento do cliente, os usuários devem usar SQL_COPT_SS_PRESERVE_CURSORS. Para obter mais informações, veja [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
Quando ativada (ON), esta opção habilita as seguintes configurações ISO:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
Juntas, essas opções SET padrão ISO definem o ambiente de processamento de consulta para a duração da sessão de trabalho do usuário, um disparador em execução ou um procedimento armazenado. Entretanto, essas opções SET não incluem todas as opções exigidas para estar de acordo com padrão ISO.  
  
Ao trabalhar com índices em colunas computadas e exibições indexadas, quatro desses padrões (ANSI_NULLS, ANSI_PADDING, ANSI_WARNINGS e QUOTED_IDENTIFIER) devem ser definidos como ON. Esses padrões estão entre as sete opções SET que devem ser atribuídas aos valores necessários para criar e alterar índices em colunas computadas e exibições indexadas. As outras opções de SET são ARITHABORT (ON), CONCAT_NULL_YIELDS_NULL (ON) e NUMERIC_ROUNDABORT (OFF). Para obter mais informações sobre as configurações da opção SET necessárias com exibições indexadas e índices em colunas computadas, confira [Considerações sobre o uso das instruções SET](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements).  
  
O driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC e o Provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem automaticamente ANSI_DEFAULTS como ON na conexão. O driver e Provedor definem CURSOR_CLOSE_ON_COMMIT e IMPLICIT_TRANSACTIONS como OFF. As configurações OFF para CURSOR_CLOSE_ON_COMMIT e IMPLICIT_TRANSACTIONS podem ser definidas nas fontes de dados ODBC, nos atributos de conexão ODBC ou nas propriedades de conexão OLE DB do aplicativo antes de conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O padrão para ANSI_DEFAULTS é OFF para conexões de aplicativos DB-Library.  
  
Quando SET ANSI_DEFAULTS é gerado, QUOTED_IDENTIFIER é definido no momento da análise e as seguintes opções são definidas em tempo de execução:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permissões  
Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir define ANSI_DEFAULTS como ON e usa a instrução `DBCC USEROPTIONS` para exibir as configurações que são afetadas.  
  
```sql  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  

-- Display the current settings.  
DBCC USEROPTIONS;  
GO 

-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
