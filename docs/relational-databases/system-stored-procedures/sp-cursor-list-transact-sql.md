---
title: sp_cursor_list (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8c6cef14177e871f35ccd5c84af4a2b28e35aff5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724041"
---
# <a name="spcursorlist-transact-sql"></a>sp_cursor_list (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa os atributos de cursores de servidor atualmente abertos para a conexão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cursor_return=] *cursor_variable_name*saída  
 É o nome de uma variável de cursor declarada. *cursor_variable_name* está **cursor**, sem padrão. O cursor é um cursor rolável, dinâmico, somente leitura.  
  
 [ @cursor_scope= ] *cursor_scope*  
 Especifica o nível dos cursores a serem relatados. *cursor_scope* está **int**, sem padrão e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|1|Informar todos os cursores locais.|  
|2|Informar todos os cursores globais.|  
|3|Informar cursores locais e globais.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="cursors-returned"></a>Cursores retornados  
 sp_cursor_list retorna seu relatório como um parâmetro de saída de cursor [!INCLUDE[tsql](../../includes/tsql-md.md)], não como um conjunto de resultados. Isso permite que lotes, procedimentos armazenados e gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] funcionem com a saída, uma linha de cada vez. Isso também significa que o procedimento não pode ser chamado diretamente de funções API do banco de dados. O parâmetro de saída de cursor deve ser associado a uma variável de programa, mas as APIs do banco de dados não oferecem suporte a associações de parâmetros ou variáveis de cursor.  
  
 Esse é o formato do cursor retornado por sp_cursor_list. O formato do cursor é o mesmo que o formato retornado por sp_cursor_list.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|O nome usado para se referir ao cursor. Se a referência ao cursor for feita através do nome dado em uma instrução DECLARE CURSOR, o nome de referência será igual ao nome do cursor. Se a referência ao cursor foi feita por uma variável, o nome da referência será o nome da variável do cursor.|  
|cursor_name|**sysname**|O nome do cursor de uma instrução DECLARE CURSOR. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o cursor foi criado, definindo uma variável de cursor para um cursor **cursor_name** retorna o nome da variável de cursor.  Em versões anteriores, essa coluna de saída retorna um nome gerado pelo sistema.|  
|cursor_scope|**smallint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**smallint**|Os mesmos valores conforme informado pela função do sistema CURSOR_STATUS:<br /><br /> 1 = O cursor referenciado pelo nome do cursor ou pela variável de cursor está aberto. Se o cursor for insensível, estático ou controlado por um conjunto de chaves terá ao menos uma linha. Se o cursor for dinâmico, o conjunto de resultados terá zero ou mais linhas.<br /><br /> 0 = O cursor referenciado pelo nome ou pela variável do cursor está aberto, mas não contém linhas. Cursores dinâmicos nunca retornam esse valor.<br /><br /> -1 = O cursor referenciado pelo nome ou pela variável do cursor está fechado.<br /><br /> -2 = Aplicável somente a variáveis de cursor. Não há nenhum cursor atribuído à variável. Possivelmente, um parâmetro OUTPUT atribuiu um cursor à variável, mas o procedimento armazenado fechou o cursor antes de retornar.<br /><br /> -3 = Um cursor ou uma variável de cursor com o nome especificado não existe, ou nenhum cursor foi alocado à variável de cursor.|  
|modelo|**smallint**|1 = Insensível (ou estático)<br /><br /> 2 = conjunto de chaves<br /><br /> 3 = dinâmico<br /><br /> 4 = De avanço rápido|  
|simultaneidade|**smallint**|1 = somente leitura<br /><br /> 2 = Bloqueios de rolagem<br /><br /> 3 = Otimista|  
|rolável|**smallint**|0 = Somente avanço<br /><br /> 1 = Rolável|  
|open_status|**smallint**|0 = Fechado<br /><br /> 1 = Abrir|  
|cursor_rows|**int**|O número de linhas de qualificação no conjunto de resultados. Para obter mais informações, consulte [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|O status da última busca nesse cursor. Para obter mais informações, consulte [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md):<br /><br /> 0 = Busca bem-sucedida.<br /><br /> -1 = A busca falhou ou está além dos limites do cursor.<br /><br /> -2 = A linha solicitada está ausente.<br /><br /> -9 = Não houve busca no cursor.|  
|column_count|**smallint**|O número de colunas no conjunto de resultados do cursor.|  
|row_count|**smallint**|O número de linhas afetadas pela última operação no cursor. Para obter mais informações, consulte [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**smallint**|A última operação executada no cursor:<br /><br /> 0 = Nenhuma operação foi executada no cursor.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = INSERIR<br /><br /> 4 = UPDATE<br /><br /> 5 = EXCLUIR<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Um valor exclusivo que identifica o cursor dentro do escopo do servidor.|  
  
## <a name="remarks"></a>Comentários  
 sp_cursor_list gera uma lista dos cursores de servidor atuais aberta pela conexão e descreve os atributos globais de cada cursor, como a capacidade do cursor de ser rolável e atualizável. Os cursores listados por sp_cursor_list incluem:  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]Cursores de servidor   
  
-   Cursores de servidor API abertos por um aplicativo ODBC que é chamado SQLSetCursorName para o nome do cursor.  
  
 Use sp_describe_cursor_columns para uma descrição dos atributos do conjunto de resultados retornado pelo cursor. Use sp_describe_cursor_tables para obter um relatório das tabelas base referenciadas pelo cursor. sp_describe_cursor reporta as mesmas informações que sp_cursor_list, mas apenas para um cursor especificado.  
  
## <a name="permissions"></a>Permissões  
 Execute permissões padrão para a função pública.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre um cursor global e usa `sp_cursor_list` para informar os atributos do cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
