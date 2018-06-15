---
title: sp_describe_cursor_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_tables_TSQL
- sp_describe_cursor_tables
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_tables
ms.assetid: 02c0f81a-54ed-4ca4-aa4f-bb7463a9ab9a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 767cf7be622e557f78e207cfc8fecb9c4b0707e9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261861"
---
# <a name="spdescribecursortables-transact-sql"></a>sp_describe_cursor_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa os objetos ou tabelas base referenciadas por um cursor de servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_describe_cursor_tables   
     [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
     , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
     , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cursor_return=] *output_cursor_variable*saída  
 É o nome de uma variável de cursor declarada para recebimento da saída do cursor. *output_cursor_variable* é **cursor**, sem padrão e deve não ser associado a qualquer cursor no momento sp_describe_cursor_tables é chamado. O cursor retornado é um cursor rolável, dinâmico, somente leitura.  
  
 [ @cursor_source=] {N'local' | N'global' | N'variable'}  
 Especifica se o cursor que está sendo relatado foi especificado usando o nome de um cursor local, de um cursor global ou de uma variável de cursor. O parâmetro é **nvarchar (30)**.  
  
 [ @cursor_identity=] N'*local_cursor_name*'  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR que tem a palavra-chave LOCAL, ou que adotou o padrão LOCAL. *local_cursor_name* é **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*global_cursor_name*'  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR que tem a palavra-chave GLOBAL, ou que adotou GLOBAL como padrão. *global_cursor_name* também pode ser o nome de um cursor de servidor API aberto por um aplicativo ODBC que então nomeou o cursor chamando SQLSetCursorName. *global_cursor_name* é **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*input_cursor_variable*'  
 É o nome de uma variável de cursor associada a um cursor aberto. *input_cursor_variable* é **nvarchar (128)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="cursors-returned"></a>Cursores retornados  
 sp_describe_cursor_tables encapsula seu relatório como um [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor** parâmetro de saída. Isso permite que lotes [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimentos armazenados e gatilhos trabalhem com a saída uma linha de cada vez. Isso também significa que o procedimento não pode ser chamado diretamente de funções API. O **cursor** parâmetro de saída deve ser associado a uma variável de programa, mas as APIs não oferecem suporte a ligação **cursor** parâmetros ou variáveis.  
  
 A tabela a seguir mostra o formato do cursor retornado por sp_describe_cursor_tables.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|table owner|**sysname**|ID de usuário do proprietário de tabela.|  
|table_name|**sysname**|Nome do objeto ou tabela base. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cursores de servidor sempre retornam o objeto especificado pelo usuário, não as tabelas base.|  
|Optimizer_hints|**smallint**|Bitmap constituído de um ou mais dos seguinte itens:<br /><br /> 1 = Bloqueio de nível de linha (ROWLOCK)<br /><br /> 4 = Bloqueio em nível de página (PAGELOCK)<br /><br /> 8 = Bloqueio de tabela (TABLOCK)<br /><br /> 16 = Bloqueio de tabela exclusivo (TABLOCKX)<br /><br /> 32 = Update lock (UPDLOCK)<br /><br /> 64 = Sem bloqueio (NOLOCK)<br /><br /> 128 = Opção primeira-linha rápida (FASTFIRST)<br /><br /> 4096 = Semântica de repetição de leitura, quando usado com DECLARE CURSOR (HOLDLOCK)<br /><br /> Quando são fornecidas diversas opções, o sistema usa a mais restritiva. No entanto, sp_describe_cursor_tables mostra os sinalizadores especificados na consulta.|  
|lock_type|**smallint**|Tipo de scroll lock solicitado, explícita ou implicitamente, para cada tabela base subjacente a este cursor. O valor pode ser um dos seguintes:<br /><br /> 0 = Nenhum<br /><br /> 1 = Compartilhado<br /><br /> 3 = atualizar|  
|server_name|**sysname, anulável**|Nome do servidor vinculado em que reside a tabela. NULL quando OPENQUERY ou OPENROWSET são usados.|  
|Objectid|**Int**|ID do objeto da tabela. 0 quando OPENQUERY ou OPENROWSET são usados.|  
|dbid|**Int**|ID do banco de dados em que a tabela reside. 0 quando OPENQUERY ou OPENROWSET são usados.|  
|dbname|**sysname**, **anulável**|Nome do banco de dados em que a tabela reside. NULL quando OPENQUERY ou OPENROWSET são usados.|  
  
## <a name="remarks"></a>Remarks  
 sp_describe_cursor_tables descreve as tabelas base referenciadas por um cursor de servidor. Para obter uma descrição dos atributos do conjunto de resultados retornado pelo cursor, use sp_describe_cursor_columns. Para obter uma descrição das características globais do cursor, como sua rolagem e atualização, use sp_describe_cursor. Para obter um relatório do [!INCLUDE[tsql](../../includes/tsql-md.md)] cursores de servidor que estão visíveis na conexão, use sp_cursor_list.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre um cursor global e usa `sp_describe_cursor_tables` para informar as tabelas referenciadas pelo cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
  
OPEN abc;  
GO  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_tables.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_tables into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_tables  
      @cursor_return = @Report OUTPUT,  
      @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_tables output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_tables.  
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
 [CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
