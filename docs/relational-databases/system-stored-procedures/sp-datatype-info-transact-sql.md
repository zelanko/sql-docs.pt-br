---
title: sp_datatype_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
author: stevestein
ms.author: sstein
ms.openlocfilehash: 39e8f688c23cffb1512be1cd1142d38c010668a7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108302"
---
# <a name="sp_datatype_info-transact-sql"></a>sp_datatype_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Retorna informações sobre os tipos de dados para os quais o ambiente atual oferece suporte.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @data_type = ] data_type`É o número de código para o tipo de dados especificado. Para obter uma lista de todos os tipos de dados, omita este parâmetro. *data_type* é **int**, com um padrão de 0.  
  
`[ @ODBCVer = ] odbc_version`É a versão do ODBC que é usada. *odbc_version* é **tinyint**, com um padrão de 2.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|Tipo de dados dependente do DBMS.|  
|DATA_TYPE|**smallint**|Código do tipo ODBC para o qual são mapeadas todas as colunas deste tipo.|  
|PRECISION|**int**|Precisão máxima do tipo de dados na fonte de dados. NULL é retornado para os tipos de dados para os quais a precisão não é aplicável. O valor de retorno da coluna PRECISION está na base 10.|  
|LITERAL_PREFIX|**varchar (** 32 **)**|Caractere ou caracteres usados antes de uma constante. Por exemplo, uma aspa simples (**'**) para tipos de caracteres e 0x para Binary.|  
|LITERAL_SUFFIX|**varchar (** 32 **)**|Caractere ou caracteres usados para terminar uma constante. Por exemplo, uma aspa simples (**'**) para tipos de caracteres e sem aspas para binário.|  
|CREATE_PARAMS|**varchar (** 32 **)**|Descrição dos parâmetros de criação para este tipo de dados. Por exemplo, **decimal** é "Precision, Scale", **float** é NULL e **varchar** é "max_length".|  
|NULLABLE|**smallint**|Especifica possibilidade de nulidade:<br /><br /> 1 = Permite valores nulos.<br /><br /> 0 = Não permite valores nulos.|  
|CASE_SENSITIVE|**smallint**|Especifica diferenciação de maiúsculas e minúsculas.<br /><br /> 1 = Todas as colunas deste tipo fazem diferenciação de maiúsculas e minúsculas (para ordenações).<br /><br /> 0 = Todas as colunas deste tipo não fazem distinção entre maiúsculas e minúsculas.|  
|SEARCHABLE|**smallint**|Especifica o recurso de pesquisa do tipo de coluna:<br /><br /> 1 = Não pode ser pesquisado.<br /><br /> 2 = Pesquisável com LIKE.<br /><br /> 3 = Pesquisável com WHERE.<br /><br /> 4 = Pesquisável com WHERE ou LIKE.|  
|UNSIGNED_ATTRIBUTE|**smallint**|Especifica o sinal do tipo de dados.<br /><br /> 1 = Tipo de dados não assinado.<br /><br /> 0 = Tipo de dados assinado.|  
|MONEY|**smallint**|Especifica o tipo de dados **Money** .<br /><br /> 1 = tipo de dados **Money** .<br /><br /> 0 = não é um tipo de dados **Money** .|  
|AUTO_INCREMENT|**smallint**|Especifica incremento automático.<br /><br /> 1 = Incremento automático.<br /><br /> 0 = Não tem incremento automático.<br /><br /> NULL = Atributo não aplicável.<br /><br /> Um aplicativo pode inserir valores em uma coluna que tenha esse atributo, mas o aplicativo não pode atualizar os valores da coluna. Com exceção do tipo de dados **bit** , AUTO_INCREMENT é válido somente para os tipos de dados que pertencem às categorias exatas de tipo de dados numeric e aproximado.|  
|LOCAL_TYPE_NAME|**sysname**|Versão localizada do nome do tipo de dados dependente da fonte de dados. Por exemplo, DECIMAL é DECIMALE em francês. NULL será retornado se a fonte de dados não oferecer suporte a um nome localizado.|  
|MINIMUM_SCALE|**smallint**|Escala mínima do tipo de dados na fonte de dados. Se um tipo de dados tiver uma escala fixa, as colunas MINIMUM_SCALE e MAXIMUM_SCALE conterão esse valor. NULL será retornado onde escala não for aplicável.|  
|MAXIMUM_SCALE|**smallint**|Escala máxima do tipo de dados na fonte de dados. Se a escala máxima não estiver definida separadamente na fonte de dados, mas em vez disso estiver definida como sendo a mesma que a precisão máxima, esta coluna conterá o mesmo valor que a coluna PRECISION.|  
|SQL_DATA_TYPE|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Essa coluna é igual à DATA_TYPE coluna, exceto para os tipos de dados **DateTime** e **intervalo** ANSI. Esse campo sempre retorna um valor.|  
|SQL_DATETIME_SUB|**smallint**|subcódigo de **data/hora** ou **intervalo** ANSI se o valor de SQL_DATA_TYPE for SQL_DATETIME ou SQL_INTERVAL. Para tipos de dados diferentes de **DateTime** e **intervalo**ANSI, esse campo é nulo.|  
|NUM_PREC_RADIX|**int**|Número de bits ou dígitos para calcular o número máximo que uma coluna pode conter. Se o tipo de dados for numérico aproximado, esta coluna conterá o valor 2 para indicar vários bits. Para tipos numéricos exatos, esta coluna contém o valor 10 para indicar vários dígitos decimais. Caso contrário, esta coluna será NULL. Ao combinar a precisão com a base, o aplicativo pode calcular o número máximo que a coluna pode conter.|  
|INTERVAL_PRECISION|**smallint**|Valor da precisão inicial do intervalo se *data_type* for **intervalo**; caso contrário, NULL.|  
|USERTYPE|**smallint**|valor **UserType** da tabela systypes.|  
  
## <a name="remarks"></a>Comentários  
 sp_datatype_info é equivalente a SQLGetTypeInfo no ODBC. Os resultados retornados são ordenados por DATA_TYPE e depois pela proximidade com que o tipo de dados é mapeado ao tipo de dados ODBC SQL correspondente.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera informações para os tipos de dados **sysname** e **nvarchar** especificando o valor de `-9` *data_type* de.  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
