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
ms.openlocfilehash: f82fc9006012d55902f1b5b3260dc7012fd6640a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053067"
---
# <a name="sp_describe_cursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa os atributos de um cursor de servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @cursor_return= ] *output_cursor_variable* DER  
 É o nome de uma variável de cursor declarada para recebimento da saída do cursor. *output_cursor_variable* é **cursor**, sem padrão, e não deve ser associado a nenhum cursores no momento sp_describe_cursor é chamado. O cursor retornado é um cursor rolável, dinâmico, somente leitura.  
  
 [ @cursor_source= ] {N'local ' | N'global ' | N'variable' }  
 Especifica se o cursor que está sendo relatado foi especificado usando o nome de um cursor local, de um cursor global ou de uma variável de cursor. O parâmetro é **nvarchar (30)**.  
  
 [ @cursor_identity= ] N '*local_cursor_name*']  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave LOCAL ou que adotou o padrão LOCAL. *local_cursor_name* é **nvarchar (128)**.  
  
 [ @cursor_identity= ] N '*global_cursor_name*']  
 É o nome de um cursor criado por uma instrução DECLARE CURSOR, que tem a palavra-chave GLOBAL ou que adotou o padrão GLOBAL. *global_cursor_name* é **nvarchar (128)**.  
  
 *global_cursor_name* também pode ser o nome de um cursor do servidor de API que é aberto por um aplicativo ODBC que, em seguida, nomeado chamando SQLSetCursorName.  
  
 [ @cursor_identity= ] N '*input_cursor_variable*']  
 É o nome de uma variável de cursor associada a um cursor aberto. *input_cursor_variable* é **nvarchar (128)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="cursors-returned"></a>Cursores retornados  
 sp_describe_cursor encapsula seu conjunto de resultados em um [!INCLUDE[tsql](../../includes/tsql-md.md)] parâmetro de saída de **cursor** . Isso permite que lotes [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimentos armazenados e gatilhos trabalhem com a saída uma linha de cada vez. Isto também significa que o procedimento não pode ser chamado diretamente de funções da API de banco de dados. O parâmetro de saída do **cursor** deve ser associado a uma variável de programa, mas as APIs de banco de dados não dão suporte a parâmetros ou variáveis de **cursor** de associação.  
  
 A tabela a seguir mostra o formato do cursor retornado ao se usar sp_describe_cursor. O formato do cursor é o mesmo formato retornado ao se usar sp_cursor_list.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|Nome usado para se referir ao cursor. Se a referência ao cursor for feita através do nome especificado em uma instrução DECLARE CURSOR, o nome de referência será igual ao nome de cursor. Se a referência ao cursor for feita por uma variável, o nome de referência será o nome da variável.|  
|cursor_name|**sysname**|Nome do cursor de uma instrução DECLARE CURSOR. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o cursor tiver sido criado pela definição de uma variável de cursor para um cursor, cursor_name retornará o nome da variável de cursor. Em versões mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa coluna de saída retorna um nome gerado pelo sistema.|  
|cursor_scope|**tinyint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**int**|Mesmos valores como relatado pela função do sistema CURSOR_STATUS:<br /><br /> 1 = O cursor referenciado pelo nome do cursor ou pela variável de cursor está aberto. Se o cursor for insensível, estático ou controlado por um conjunto de chaves terá ao menos uma linha. Se o cursor for dinâmico, o conjunto de resultados terá zero ou mais linhas.<br /><br /> 0 = O cursor referenciado pelo nome ou pela variável do cursor está aberto, mas não contém linhas. Cursores dinâmicos nunca retornam esse valor.<br /><br /> -1 = O cursor referenciado pelo nome ou pela variável do cursor está fechado.<br /><br /> -2 = Aplicável somente a variáveis de cursor. Não há nenhum cursor atribuído à variável. Possivelmente, um parâmetro OUTPUT atribuiu um cursor à variável, mas o procedimento armazenado fechou o cursor antes de retornar.<br /><br /> -3 = Um cursor ou uma variável de cursor com o nome especificado não existe, ou nenhum cursor foi alocado à variável de cursor.|  
|modelo|**tinyint**|1 = Insensível (ou estático)<br /><br /> 2 = conjunto de chaves<br /><br /> 3 = dinâmico<br /><br /> 4 = De avanço rápido|  
|simultaneidade|**tinyint**|1 = somente leitura<br /><br /> 2 = Bloqueios de rolagem<br /><br /> 3 = Otimista|  
|rolável|**tinyint**|0 = Somente avanço<br /><br /> 1 = Rolável|  
|open_status|**tinyint**|0 = Fechado<br /><br /> 1 = Abrir|  
|cursor_rows|**decimal (10, 0)**|Número de linhas de qualificação no conjunto de resultados. Para obter mais informações, consulte [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|Status da última busca nesse cursor. Para obter mais informações, consulte [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md).<br /><br /> 0 = Busca bem-sucedida.<br /><br /> -1 = A busca falhou ou está além dos limites do cursor.<br /><br /> -2 = A linha solicitada está ausente.<br /><br /> -9 = Não houve busca no cursor.|  
|column_count|**smallint**|Número de colunas no conjunto de resultados do cursor.|  
|row_count|**decimal (10, 0)**|Número de linhas afetadas pela última operação no cursor. Para obter mais informações, consulte [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**tinyint**|Última operação executada no cursor:<br /><br /> 0 = Nenhuma operação foi executada no cursor.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = INSERIR<br /><br /> 4 = UPDATE<br /><br /> 5 = EXCLUIR<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Um valor exclusivo para o cursor dentro do escopo do servidor.|  
  
## <a name="remarks"></a>Comentários  
 sp_describe_cursor descreve os atributos globais a um cursor de servidor, como a habilidade para rolar e atualizar. Use sp_describe_cursor_columns para uma descrição dos atributos do conjunto de resultados retornado pelo cursor. Use sp_describe_cursor_tables para obter um relatório das tabelas base referenciadas pelo cursor. Para obter um relatório dos cursores de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)] visíveis na conexão, use sp_cursor_list.  
  
 Uma instrução DECLARE CURSOR pode exigir um tipo de cursor que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não suporta usando a instrução SELECT que está contida no DECLARE CURSOR. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte o cursor implicitamente a um tipo que ofereça suporte para usar a instrução SELECT. Se TYPE_WARNING for especificado na instrução DECLARE CURSOR, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enviará ao aplicativo uma mensagem informativa de que uma conversão foi concluída. sp_describe_cursor pode ser chamado para determinar o tipo de cursor que foi implementado.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Cursores](../../relational-databases/cursors.md)   
 [&#41;&#40;Transact-SQL de CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursor_list](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_describe_cursor_columns](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_describe_cursor_tables](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
