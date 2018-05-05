---
title: sp_datatype_info (Transact-SQL) | Microsoft Docs
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
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 868d88651994ea31e118569a02236edde712ccad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdatatypeinfo-transact-sql"></a>sp_datatype_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os tipos de dados para os quais o ambiente atual oferece suporte.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@data_type=** ] *data_type*  
 É o número de código do tipo de dados especificado. Para obter uma lista de todos os tipos de dados, omita este parâmetro. *data_type* é **int**, com um padrão de 0.  
  
 [ **@ODBCVer=** ] *odbc_version*  
 É a versão do ODBC usada. *odbc_version* é **tinyint**, com um padrão de 2.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|Tipo de dados dependente do DBMS.|  
|DATA_TYPE|**smallint**|Código do tipo ODBC para o qual são mapeadas todas as colunas deste tipo.|  
|PRECISION|**Int**|Precisão máxima do tipo de dados na fonte de dados. NULL é retornado para os tipos de dados para os quais a precisão não é aplicável. O valor de retorno da coluna PRECISION está na base 10.|  
|LITERAL_PREFIX|**varchar(** 32 **)**|Caractere ou caracteres usados antes de uma constante. Por exemplo, uma aspa simples (**'**) para tipos de caractere e 0x para binário.|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|Caractere ou caracteres usados para terminar uma constante. Por exemplo, uma aspa simples (**'**) para tipos de caractere e nenhuma aspa para binário.|  
|CREATE_PARAMS|**varchar(** 32 **)**|Descrição dos parâmetros de criação para este tipo de dados. Por exemplo, **decimal** é "precisão, escala", **float** for NULL, e **varchar** é "max_length".|  
|NULLABLE|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = Permite valores nulos.<br /><br /> 0 = Não permite valores nulos.|  
|CASE_SENSITIVE|**smallint**|Especifica diferenciação de maiúsculas e minúsculas.<br /><br /> 1 = Todas as colunas deste tipo fazem diferenciação de maiúsculas e minúsculas (para agrupamentos).<br /><br /> 0 = Todas as colunas deste tipo não fazem distinção entre maiúsculas e minúsculas.|  
|SEARCHABLE|**smallint**|Especifica o recurso de pesquisa do tipo de coluna:<br /><br /> 1 = Não pode ser pesquisado.<br /><br /> 2 = Pesquisável com LIKE.<br /><br /> 3 = Pesquisável com WHERE.<br /><br /> 4 = Pesquisável com WHERE ou LIKE.|  
|UNSIGNED_ATTRIBUTE|**smallint**|Especifica o sinal do tipo de dados.<br /><br /> 1 = Tipo de dados não assinado.<br /><br /> 0 = Tipo de dados assinado.|  
|MONEY|**smallint**|Especifica o **money** tipo de dados.<br /><br /> 1 = **money** tipo de dados.<br /><br /> 0 = não uma **money** tipo de dados.|  
|AUTO_INCREMENT|**smallint**|Especifica incremento automático.<br /><br /> 1 = Incremento automático.<br /><br /> 0 = Não tem incremento automático.<br /><br /> NULL = Atributo não aplicável.<br /><br /> Um aplicativo pode inserir valores em uma coluna que tenha esse atributo, mas o aplicativo não pode atualizar os valores da coluna. Com exceção do **bit** tipo de dados, AUTO_INCREMENT é válido somente para tipos de dados que pertencem a numérico exato e numérico aproximado categorias de tipo de dados.|  
|LOCAL_TYPE_NAME|**sysname**|Versão localizada do nome do tipo de dados dependente da fonte de dados. Por exemplo, DECIMAL é DECIMALE em francês. NULL será retornado se a fonte de dados não oferecer suporte a um nome localizado.|  
|MINIMUM_SCALE|**smallint**|Escala mínima do tipo de dados na fonte de dados. Se um tipo de dados tiver uma escala fixa, as colunas MINIMUM_SCALE e MAXIMUM_SCALE conterão esse valor. NULL será retornado onde escala não for aplicável.|  
|MAXIMUM_SCALE|**smallint**|Escala máxima do tipo de dados na fonte de dados. Se a escala máxima não estiver definida separadamente na fonte de dados, mas em vez disso estiver definida como sendo a mesma que a precisão máxima, esta coluna conterá o mesmo valor que a coluna PRECISION.|  
|SQL_DATA_TYPE|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é igual à coluna DATA_TYPE, exceto para o **datetime** e ANSI **intervalo** tipos de dados. Esse campo sempre retorna um valor.|  
|SQL_DATETIME_SUB|**smallint**|**DateTime** ou ANSI **intervalo** subcódigo se o valor de SQL_DATA_TYPE for SQL_DATETIME ou SQL_INTERVAL. Para tipos de dados diferente de **datetime** e ANSI **intervalo**, este campo é NULL.|  
|NUM_PREC_RADIX|**Int**|Número de bits ou dígitos para calcular o número máximo que uma coluna pode conter. Se o tipo de dados for numérico aproximado, esta coluna conterá o valor 2 para indicar vários bits. Para tipos numéricos exatos, esta coluna contém o valor 10 para indicar vários dígitos decimais. Caso contrário, esta coluna será NULL. Ao combinar a precisão com a base, o aplicativo pode calcular o número máximo que a coluna pode conter.|  
|INTERVAL_PRECISION|**smallint**|Valor de intervalo de precisão principal se *data_type* é **intervalo**; caso contrário, NULL.|  
|USERTYPE|**smallint**|**usertype** valor da tabela systypes.|  
  
## <a name="remarks"></a>Remarks  
 sp_datatype_info é equivalente à SQLGetTypeInfo no ODBC. Os resultados retornados são ordenados por DATA_TYPE e depois pela proximidade com que o tipo de dados é mapeado ao tipo de dados ODBC SQL correspondente.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera informações para o **sysname** e **nvarchar** tipos de dados, especificando o *data_type* valor de `-9`.  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
