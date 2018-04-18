---
title: sp_batch_params (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9843453dce8234e97b40e3ca3be45ed1e48d7c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spbatchparams-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de linhas que contém informações sobre os parâmetros incluídos em um [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. **sp_batch_params** somente analisa o lote especificado e retorna informações sobre valores de parâmetros inseridos. Ele não executa o lote ou modifica o ambiente de execução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tsqlbatch =**] **'***tsqlbatch***'**  
 É uma cadeia de caracteres Unicode que contém um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote para quais informações são que você deseja. *tsqlbatch* é **nvarchar (max)** ou implicitamente conversível em **nvarchar (max)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|Nome do parâmetro que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou no lote.|  
|**COLUMN_TYPE**|**smallint**|Este campo retorna um dos valores seguintes:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> Esta coluna é sempre 0.|  
|**DATA_TYPE**|**smallint**|Tipo de dados do parâmetro (código Inteiro para um tipo de dados do ODBC). Se este tipo de dados não puder ser mapeado para um tipo ISO, o valor será NULL. O nome do tipo de dados nativo é retornado no **TYPE_NAME** coluna. Esse valor é sempre NULL.|  
|**TYPE_NAME**|**sysname**|Representação em cadeia de caracteres do tipo de dados, como é apresentado pelo DBMS subjacente. Esse valor será NULL.|  
|**PRECISION**|**Int**|Número de dígitos significativos. O valor de retorno para o **precisão** coluna está na base 10.|  
|**LENGTH**|**Int**|Tamanho da transferência dos dados. Esse valor será NULL.|  
|**ESCALA**|**smallint**|Número de dígitos à direita da vírgula decimal. Esse valor será NULL.|  
|**BASE**|**smallint**|É a base para tipos numéricos. Esse valor será NULL.|  
|**PERMITE VALOR NULO**|**smallint**|Especifica a condição de nulidade:<br /><br /> 1 = O tipo de dados do parâmetro pode ser criado permitindo valores nulos.<br /><br /> 0 = Não são permitidos valores nulos.<br /><br /> Esse valor será NULL.|  
|**SQL_DATA_TYPE**|**smallint**|Valor do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ele aparece no campo TYPE do descritor. Essa coluna é o mesmo que o **DATA_TYPE** coluna, exceto para o **datetime** e ISO **intervalo** tipos de dados. Esta coluna sempre retorna um valor. Esse valor será NULL.|  
|**SQL_DATETIME_SUB**|**smallint**|O **datetime** ou ISO **intervalo** subcódigo se o valor de **SQL_DATA_TYPE** for SQL_DATETIME ou SQL_INTERVAL. Para tipos de dados diferente de **datetime** e ISO **intervalo**, essa coluna será NULL. Esse valor será NULL.|  
|**CHAR_OCTET_LENGTH**|**Int**|Tamanho máximo em bytes de um **caracteres** ou **binário** parâmetro de tipo de dados. Para todos os outros tipos de dados, esta coluna retorna um valor nulo. Esse valor é sempre NULL.|  
|**ORDINAL_POSITION**|**Int**|A posição ordinal do parâmetro no lote. Se o nome de parâmetro for repetido várias vezes, esta coluna conterá o ordinal da primeira ocorrência. O primeiro parâmetro tem ordinal 1. Esta coluna sempre retorna um valor.|  
  
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
 [Tópicos de instruções de procedimentos armazenados de execução &#40;ODBC&#41;](http://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [Em execução procedimentos armazenados & #40; OLE DB & #41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
