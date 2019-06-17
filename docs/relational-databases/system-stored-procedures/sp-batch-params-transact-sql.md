---
title: sp_batch_params (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b66e8b2d1b0d397a24c4ff5c702c00aff14988d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62996167"
---
# <a name="spbatchparams-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de linhas que contém informações sobre os parâmetros incluídos em um [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. **sp_batch_params** apenas analisa o lote especificado e retorna informações sobre valores de parâmetro inseridos. Ele não executa o lote ou modifica o ambiente de execução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tsqlbatch = ] 'tsqlbatch'` É uma cadeia de caracteres Unicode que contém um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote para o qual parâmetro informações são que você deseja. *tsqlbatch* está **nvarchar (max)** ou implicitamente conversível em **nvarchar (max)** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|Nome do parâmetro que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou no lote.|  
|**COLUMN_TYPE**|**smallint**|Este campo retorna um dos valores seguintes:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> Esta coluna é sempre 0.|  
|**DATA_TYPE**|**smallint**|Tipo de dados do parâmetro (código Inteiro para um tipo de dados do ODBC). Se este tipo de dados não puder ser mapeado para um tipo ISO, o valor será NULL. O nome do tipo de dados nativo é retornado na **TYPE_NAME** coluna. Esse valor é sempre NULL.|  
|**TYPE_NAME**|**sysname**|Representação em cadeia de caracteres do tipo de dados, como é apresentado pelo DBMS subjacente. Esse valor será NULL.|  
|**PRECISION**|**int**|Número de dígitos significativos. O valor retornado para o **precisão** coluna está na base 10.|  
|**LENGTH**|**int**|Tamanho da transferência dos dados. Esse valor será NULL.|  
|**ESCALA**|**smallint**|Número de dígitos à direita da vírgula decimal. Esse valor será NULL.|  
|**RADIX**|**smallint**|É a base para tipos numéricos. Esse valor será NULL.|  
|**NULLABLE**|**smallint**|Especifica a condição de nulidade:<br /><br /> 1 = O tipo de dados do parâmetro pode ser criado permitindo valores nulos.<br /><br /> 0 = Não são permitidos valores nulos.<br /><br /> Esse valor será NULL.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ele aparece no campo TYPE do descritor. Esta coluna é igual à coluna **DATA_TYPE**, com exceção dos tipos de dados **datetime** e **interval** ISO. Esta coluna sempre retorna um valor. Esse valor será NULL.|  
|**SQL_DATETIME_SUB**|**smallint**|O **datetime** ou ISO **intervalo** subcódigo se o valor de **SQL_DATA_TYPE** for SQL_DATETIME ou SQL_INTERVAL. Para tipos de dados diferente de **datetime** e ISO **intervalo**, essa coluna será NULL. Esse valor será NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Comprimento máximo em bytes de um **caractere** ou **binário** parâmetro de tipo de dados. Para todos os outros tipos de dados, esta coluna retorna um valor nulo. Esse valor é sempre NULL.|  
|**ORDINAL_POSITION**|**int**|A posição ordinal do parâmetro no lote. Se o nome de parâmetro for repetido várias vezes, esta coluna conterá o ordinal da primeira ocorrência. O primeiro parâmetro tem ordinal 1. Esta coluna sempre retorna um valor.|  
  
## <a name="permissions"></a>Permissões  
 Permissão para executar **sp_batch_params** é concedida a **público**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra uma consulta sendo passada para `sp_batch_params`. O conjunto de resultados enumera a lista de valores de parâmetro inseridos.  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executando procedimentos armazenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Executando procedimentos armazenados tópicos de instruções &#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [Executando procedimentos armazenados &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
