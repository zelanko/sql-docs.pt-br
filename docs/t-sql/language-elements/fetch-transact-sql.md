---
title: FETCH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FETCH
- FETCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- cursors [SQL Server], fetching
- Transact-SQL cursors, fetching and scrolling
- retrieving rows
- fetching [SQL Server]
- SCROLL option
- row fetching [SQL Server]
ms.assetid: 5d68dac2-f91b-4342-bb4e-209ee132665f
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd770d8f1af098d4328df12a11cdcff609f2328
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71974401"
---
# <a name="fetch-transact-sql"></a>FETCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Recupera uma linha específica de um cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FETCH   
          [ [ NEXT | PRIOR | FIRST | LAST   
                    | ABSOLUTE { n | @nvar }   
                    | RELATIVE { n | @nvar }   
               ]   
               FROM   
          ]   
{ { [ GLOBAL ] cursor_name } | @cursor_variable_name }   
[ INTO @variable_name [ ,...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 NEXT  
 Retorna a linha de resultado imediatamente seguinte à linha atual e adiciona a linha atual à linha retornada. Se `FETCH NEXT` for a primeira busca de um cursor, a primeira linha do conjunto de resultados será retornada. `NEXT` é a opção padrão de busca de cursor.  
  
 PRIOR  
 Retorna a linha de resultado imediatamente anterior à linha atual e decrementa a linha atual da linha retornada. Se `FETCH PRIOR` for a primeira busca de um cursor, nenhuma linha será retornada e o cursor será deixado posicionado antes da primeira linha.  
  
 FIRST  
 Retorna a primeira linha no cursor e a torna a linha atual.  
  
 LAST  
 Retorna a última linha no cursor e a torna a linha atual.  
  
 ABSOLUTE { *n*| \@*nvar*}  
 Se *n* ou \@*nvar* for positivo, retornará a linha que está *n* linhas da frente do cursor e tornará a linha retornada a nova linha atual. Se *n* ou \@*nvar* for negativo, retornará a linha que está *n* linhas antes do final do cursor e tornará a linha retornada a nova linha atual. Se *n* ou \@*nvar* for 0, nenhuma linha será retornada. *n* precisa ser uma constante de inteiro e \@*nvar* precisa ser **smallint**, **tinyint** ou **int**.  
  
 RELATIVE { *n*| \@*nvar*}  
 Se *n* ou \@*nvar* for positivo, retornará a linha que está *n* linhas após a linha atual e tornará a linha retornada a nova linha atual. Se *n* ou \@*nvar* for negativo, retornará a linha que está *n* linhas antes da linha atual e tornará a linha retornada a nova linha atual. Se *n* ou \@*nvar* for 0, retornará a linha atual. Se `FETCH RELATIVE` for especificado com *n* ou \@*nvar* definido como números negativos ou 0 no primeiro fetch feito em um cursor, nenhuma linha será retornada. *n* precisa ser uma constante de inteiro e \@*nvar* precisa ser **smallint**, **tinyint** ou **int**.  
  
 GLOBAL  
 Especifica que *cursor_name* se refere a um cursor global.  
  
 *cursor_name*  
 É o nome do cursor aberto a partir do qual a busca deve ser feita. Se um cursor global e um cursor local existirem com *cursor_name* como seu nome, *cursor_name* se referirá ao cursor global, caso GLOBAL seja especificado, e ao cursor local, caso GLOBAL não seja especificado.  
  
 \@*cursor_variable_name*  
 É o nome de uma variável de cursor que faz referência ao cursor aberto a partir do qual a busca deve ser feita.  
  
 INTO \@*variable_name*[ ,...*n*]  
 Permite que os dados das colunas de uma busca sejam colocados em variáveis locais. Cada variável na lista, da esquerda para a direita, está associada à coluna correspondente no conjunto de resultados do cursor. O tipo de dados de cada variável deve corresponder ou ser uma conversão implícita com suporte do tipo de dados da coluna do conjunto de resultados correspondente. O número de variáveis deve corresponder ao número de colunas na lista de seleção do cursor.  
  
## <a name="remarks"></a>Comentários  
 Se a opção `SCROLL` não for especificada em uma instrução de estilo ISO `DECLARE CURSOR`, `NEXT` será a única opção `FETCH` com suporte. Se `SCROLL` for especificado em um estilo ISO `DECLARE CURSOR`, todas as opções `FETCH` terão suporte.  
  
 Quando as extensões de cursor DECLARE do [!INCLUDE[tsql](../../includes/tsql-md.md)] forem usadas, estas regras se aplicarão:  
  
-   Se qualquer um dos `FORWARD_ONLY` ou `FAST_FORWARD` for especificado, `NEXT` será a única opção `FETCH` com suporte.  
  
-   Se `DYNAMIC`, `FORWARD_ONLY` ou `FAST_FORWARD` não forem especificados e um de `KEYSET`, `STATIC` ou `SCROLL` forem especificados, todas as opções `FETCH` terão suporte.  
  
-   `DYNAMIC SCROLL` cursores dão suporte a todas as opções `FETCH`, exceto `ABSOLUTE`.  
  
 A função `@@FETCH_STATUS` relata o status da última instrução `FETCH`. As mesmas informações são registradas na coluna fetch_status do cursor retornado por sp_describe_cursor. Essas informações de status devem ser usadas para determinar a validade dos dados retornados por uma instrução `FETCH` antes de tentar qualquer operação nesses dados. Para obter mais informações, consulte [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 As permissões para `FETCH` são padronizadas para qualquer usuário válido.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-fetch-in-a-simple-cursor"></a>a. Usando FETCH em um cursor simples  
 O exemplo a seguir declara um cursor simples para as linhas da tabela `Person.Person` com um sobrenome que inicia com `B` e usa `FETCH NEXT` para percorrer as linhas. As instruções `FETCH` retornam o valor da coluna especificada em `DECLARE CURSOR` como um conjunto de resultados de uma linha.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch.  
FETCH NEXT FROM contact_cursor;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="b-using-fetch-to-store-values-in-variables"></a>B. Usando FETCH para armazenar valores em variáveis  
 O exemplo a seguir é semelhante ao exemplo A, com exceção de que a saída das instruções `FETCH` é armazenada em variáveis locais em vez de ser retornada diretamente para o cliente. A instrução `PRINT` combina as variáveis em uma única cadeia de caracteres e as retorna ao cliente.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Declare the variables to store the values returned by FETCH.  
DECLARE @LastName varchar(50), @FirstName varchar(50);  
  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch and store the values in variables.  
-- Note: The variables are in the same order as the columns  
-- in the SELECT statement.   
  
FETCH NEXT FROM contact_cursor  
INTO @LastName, @FirstName;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
  
   -- Concatenate and display the current values in the variables.  
   PRINT 'Contact Name: ' + @FirstName + ' ' +  @LastName  
  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor  
   INTO @LastName, @FirstName;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="c-declaring-a-scroll-cursor-and-using-the-other-fetch-options"></a>C. Declarando um cursor SCROLL e usando as outras opções de FETCH  
 O exemplo a seguir cria um cursor `SCROLL` para permitir recursos de rolagem completos por meio das opções `LAST`, `PRIOR`, `RELATIVE` e `ABSOLUTE`.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Execute the SELECT statement alone to show the   
-- full result set that is used by the cursor.  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
-- Declare the cursor.  
DECLARE contact_cursor SCROLL CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Fetch the last row in the cursor.  
FETCH LAST FROM contact_cursor;  
  
-- Fetch the row immediately prior to the current row in the cursor.  
FETCH PRIOR FROM contact_cursor;  
  
-- Fetch the second row in the cursor.  
FETCH ABSOLUTE 2 FROM contact_cursor;  
  
-- Fetch the row that is three rows after the current row.  
FETCH RELATIVE 3 FROM contact_cursor;  
  
-- Fetch the row that is two rows prior to the current row.  
FETCH RELATIVE -2 FROM contact_cursor;  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
