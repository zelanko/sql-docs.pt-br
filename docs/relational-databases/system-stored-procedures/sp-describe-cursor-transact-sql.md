---
title: sp_describe_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 256f1add5399d3e9c5795440d80670f66a096cb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651684"
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa os atributos de um cursor de servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
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
 [ @cursor_return=] *output_cursor_variable* saída  
 É o nome de uma variável de cursor declarada para recebimento da saída do cursor. *output_cursor_variable* está **cursor**, sem padrão e deve não ser associado a nenhum cursor no momento da sp_describe_cursor é chamada. O cursor retornado é um cursor rolável, dinâmico, somente leitura.  
  
 [ @cursor_source=] {N'local' | N'global' | N'variable'}  
 Especifica se o cursor que está sendo relatado foi especificado usando o nome de um cursor local, de um cursor global ou de uma variável de cursor. O parâmetro é **nvarchar (30)**.  
  
 [ @cursor_identity=] N'*local_cursor_name*']  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave LOCAL ou que adotou o padrão LOCAL. *local_cursor_name* está **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*global_cursor_name*']  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave GLOBAL ou que adotou o padrão GLOBAL. *global_cursor_name* está **nvarchar (128)**.  
  
 *global_cursor_name* também pode ser o nome de um cursor de servidor de API que é aberto por um aplicativo ODBC que então nomeou chamando SQLSetCursorName.  
  
 [ @cursor_identity=] N'*input_cursor_variable*']  
 É o nome de uma variável de cursor associada a um cursor aberto. *input_cursor_variable* está **nvarchar (128)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="cursors-returned"></a>Cursores retornados  
 sp_describe_cursor encapsula seu conjunto de resultados em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor** parâmetro de saída. Isso permite que lotes [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimentos armazenados e gatilhos trabalhem com a saída uma linha de cada vez. Isto também significa que o procedimento não pode ser chamado diretamente de funções da API de banco de dados. O **cursor** parâmetro de saída deve ser associado a uma variável de programa, mas as APIs de banco de dados não dão suporte a associação **cursor** parâmetros ou variáveis.  
  
 A tabela a seguir mostra o formato do cursor retornado usando sp_describe_cursor. O formato do cursor é o mesmo formato retornado usando sp_cursor_list.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|Nome usado para se referir ao cursor. Se a referência ao cursor for feita através do nome especificado em uma instrução DECLARE CURSOR, o nome de referência será igual ao nome de cursor. Se a referência ao cursor for feita por uma variável, o nome de referência será o nome da variável.|  
|cursor_name|**sysname**|Nome do cursor de uma instrução DECLARE CURSOR. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o cursor tiver sido criado, definindo uma variável de cursor para um cursor, cursor_name retorna o nome da variável de cursor. Em versões mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna de saída retorna um nome gerado pelo sistema.|  
|cursor_scope|**tinyint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**int**|Mesmos valores como relatado pela função do sistema CURSOR_STATUS:<br /><br /> 1 = O cursor referenciado pelo nome do cursor ou pela variável de cursor está aberto. Se o cursor for insensível, estático ou controlado por um conjunto de chaves terá ao menos uma linha. Se o cursor for dinâmico, o conjunto de resultados terá zero ou mais linhas.<br /><br /> 0 = O cursor referenciado pelo nome ou pela variável do cursor está aberto, mas não contém linhas. Cursores dinâmicos nunca retornam esse valor.<br /><br /> -1 = O cursor referenciado pelo nome ou pela variável do cursor está fechado.<br /><br /> -2 = Aplicável somente a variáveis de cursor. Não há nenhum cursor atribuído à variável. Possivelmente, um parâmetro OUTPUT atribuiu um cursor à variável, mas o procedimento armazenado fechou o cursor antes de retornar.<br /><br /> -3 = Um cursor ou uma variável de cursor com o nome especificado não existe, ou nenhum cursor foi alocado à variável de cursor.|  
|modelo|**tinyint**|1 = Insensível (ou estático)<br /><br /> 2 = conjunto de chaves<br /><br /> 3 = dinâmico<br /><br /> 4 = De avanço rápido|  
|simultaneidade|**tinyint**|1 = somente leitura<br /><br /> 2 = Bloqueios de rolagem<br /><br /> 3 = Otimista|  
|rolável|**tinyint**|0 = Somente avanço<br /><br /> 1 = Rolável|  
|open_status|**tinyint**|0 = Fechado<br /><br /> 1 = Abrir|  
|cursor_rows|**decimal(10,0)**|Número de linhas de qualificação no conjunto de resultados. Para obter mais informações, consulte [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|Status da última busca nesse cursor. Para obter mais informações, consulte [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md).<br /><br /> 0 = Busca bem-sucedida.<br /><br /> -1 = A busca falhou ou está além dos limites do cursor.<br /><br /> -2 = A linha solicitada está ausente.<br /><br /> -9 = Não houve busca no cursor.|  
|column_count|**smallint**|Número de colunas no conjunto de resultados do cursor.|  
|row_count|**decimal(10,0)**|Número de linhas afetadas pela última operação no cursor. Para obter mais informações, consulte [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**tinyint**|Última operação executada no cursor:<br /><br /> 0 = Nenhuma operação foi executada no cursor.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = INSERIR<br /><br /> 4 = UPDATE<br /><br /> 5 = EXCLUIR<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Um valor exclusivo para o cursor dentro do escopo do servidor.|  
  
## <a name="remarks"></a>Comentários  
 sp_describe_cursor descreve os atributos que são globais para um cursor de servidor, como a capacidade de rolagem e atualização. Use sp_describe_cursor_columns para uma descrição dos atributos do conjunto de resultados retornado pelo cursor. Use sp_describe_cursor_tables para obter um relatório das tabelas base referenciadas pelo cursor. Para obter um relatório dos cursores de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)] visíveis na conexão, use sp_cursor_list.  
  
 Uma instrução DECLARE CURSOR pode exigir um tipo de cursor que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não suporta usando a instrução SELECT que está contida no DECLARE CURSOR. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte o cursor implicitamente a um tipo que ofereça suporte para usar a instrução SELECT. Se TYPE_WARNING for especificado na instrução DECLARE CURSOR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enviará ao aplicativo uma mensagem informativa de que uma conversão foi concluída. sp_describe_cursor, em seguida, pode ser chamado para determinar o tipo de cursor que foi implementado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre um cursor global e usa `sp_describe_cursor` para informar os atributos do cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
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
 [sp_describe_cursor_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
