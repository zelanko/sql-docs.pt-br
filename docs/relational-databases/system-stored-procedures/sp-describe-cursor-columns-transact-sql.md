---
title: sp_describe_cursor_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fe882cf908e4ae227a486b68c54d34376164455
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdescribecursorcolumns-transact-sql"></a>sp_describe_cursor_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata os atributos das colunas no conjunto de resultados de um cursor de servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cursor_return=] *output_cursor_variable* saída  
 É o nome de uma variável de cursor declarada para recebimento da saída do cursor. *output_cursor_variable* é **cursor**, sem padrão e deve não ser associada a nenhum cursor no momento em que sp_describe_cursor_columns é chamado. O cursor retornado é um cursor rolável, dinâmico, somente leitura.  
  
 [ @cursor_source=] {N'local' | N'global' | N'variable'}  
 Especifica se o cursor que está sendo relatado foi especificado usando o nome de um cursor local, de um cursor global ou de uma variável de cursor. O parâmetro é **nvarchar (30)**.  
  
 [ @cursor_identity=] N'*local_cursor_name*'  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave LOCAL ou que adotou o padrão LOCAL. *local_cursor_name* é **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*global_cursor_name*'  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave GLOBAL ou que adotou o padrão GLOBAL. *global_cursor_name* é **nvarchar (128)**.  
  
 *global_cursor_name* também pode ser o nome de um cursor de servidor API aberto por um aplicativo ODBC e depois nomeado chamando SQLSetCursorName.  
  
 [ @cursor_identity=] N'*input_cursor_variable*'  
 É o nome de uma variável de cursor associada a um cursor aberto. *input_cursor_variable* é **nvarchar (128)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="cursors-returned"></a>Cursores retornados  
 sp_describe_cursor_columns encapsula seu relatório como um [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor** parâmetro de saída. Isso permite que lotes [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimentos armazenados e gatilhos trabalhem com a saída uma linha de cada vez. Isto também significa que o procedimento não pode ser chamado diretamente de funções da API de banco de dados. O **cursor** parâmetro de saída deve ser associado a uma variável de programa, mas os APIs do banco de dados não dão suporte à associação **cursor** parâmetros ou variáveis.  
  
 A tabela a seguir mostra o formato do cursor retornado quando se usa sp_describe_cursor_columns.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|column_name|**sysname** (nulo)|Nome atribuído à coluna do conjunto de resultados. A coluna será NULL se tiver sido especificada sem uma cláusula AS associada.|  
|ordinal_position|**int**|Posição relativa da coluna a partir da coluna mais à esquerda do conjunto de resultados. A primeira coluna está na posição 0.|  
|column_characteristics_flags|**int**|Um bitmask que indica as informações armazenadas em DBCOLUMNFLAGS no OLE DB. Pode ser um ou uma combinação dos seguintes:<br /><br /> 1 = Indicador<br /><br /> 2 = Comprimento fixo<br /><br /> 4 = Permite valor nulo<br /><br /> 8 = Controle de versão de linha<br /><br /> 16 = Coluna atualizável (defina para colunas projetadas de um cursor que não tenha uma cláusula FOR UPDATE e, se houver tal coluna, poderá ser apenas uma por cursor).<br /><br /> Quando valores do bit são combinados, as características desses valores combinados são aplicadas. Por exemplo, se o valor do bit for 6, a coluna será de comprimento fixo (2) e permitirá valor nulo (4).|  
|column_size|**int**|Tamanho máximo possível para um valor nesta coluna.|  
|data_type_sql|**smallint**|Número que indica o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da coluna.|  
|column_precision|**tinyint**|Precisão máxima da coluna conforme o *bPrecision* valor no OLE DB.|  
|column_scale|**tinyint**|Número de dígitos à direita do ponto decimal para o **numérico** ou **decimal** tipos de dados conforme o *bScale* valor no OLE DB.|  
|order_position|**int**|Se a coluna participar da ordenação do conjunto de resultados, a posição da coluna na chave de ordem relativa à coluna mais à esquerda.|  
|order_direction|**varchar (1)**(nulo)|A = A coluna está na chave de ordem e a ordenação é crescente.<br /><br /> D = A coluna está na chave de ordem e a ordenação é decrescente.<br /><br /> NULL = A coluna não participa na ordenação.|  
|hidden_column|**smallint**|0 = esta coluna aparece na lista de seleção.<br /><br /> 1 = Reservado para uso futuro.|  
|columnid|**int**|ID da coluna base. Se a coluna do conjunto de resultados foi criada a partir de uma expressão, columnid será -1.|  
|objectid|**int**|O ID do objeto ou da tabela base que está fornecendo a coluna. Se a coluna do conjunto de resultados foi criada a partir de uma expressão, objectid será -1.|  
|dbid|**int**|O ID do banco que dados que contém a tabela base que está fornecendo a coluna. Se a coluna do conjunto de resultados foi criada a partir de uma expressão, dbid será -1.|  
|dbname|**sysname**<br /><br /> (permite valor nulo)|Nome do banco que dados que contém a tabela base que está fornecendo a coluna. Se a coluna do conjunto de resultados foi criada a partir de uma expressão, dbname será NULL.|  
  
## <a name="remarks"></a>Comentários  
 sp_describe_cursor_columns descreve os atributos das colunas no conjunto de resultados de um cursor de servidor, tais como o nome e o tipo de dados de cada cursor. Use sp_describe_cursor para obter uma descrição dos atributos globais do cursor de servidor. Use sp_describe_cursor_tables para obter um relatório das tabelas base referenciadas pelo cursor. Para obter um relatório dos cursores de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)] visíveis na conexão, use sp_cursor_list.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre um cursor global e usa `sp_describe_cursor_columns` para relatar as colunas usadas no cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Cursores](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_describe_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_cursor_list &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_tables &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
