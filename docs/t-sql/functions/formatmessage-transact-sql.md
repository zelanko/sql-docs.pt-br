---
description: FORMATMESSAGE (Transact-SQL)
title: FORMATMESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 47eb4bb9e66f7f4fa9a84b694ebd8915f0c60d31
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459706"
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Constrói uma mensagem com base em uma mensagem existente em sys.messages ou em uma cadeia de caracteres fornecida. A funcionalidade de FORMATMESSAGE se assemelha à da instrução RAISERROR. Entretanto, RAISERROR imprime a mensagem imediatamente, enquanto FORMATMESSAGE retorna a mensagem formatada para processamento posterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *msg_number*  
 É a ID da mensagem armazenada em sys.messages. Se *msg_number* for <= 13.000 ou se a mensagem não existir em sys.messages, NULL será retornado.  
  
 *msg_string*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 É uma cadeia de caracteres entre aspas simples e que contém espaços reservados de valor do parâmetro. A mensagem de erro pode ter no máximo 2.047 caracteres. Se a mensagem tiver 2.048 caracteres ou mais, somente os primeiros 2.044 serão exibidos e um sinal de reticências será adicionado para indicar que a mensagem foi truncada. Observe que os parâmetros de substituição consomem mais caracteres que a saída mostra por causa de comportamento de armazenamento interno.  Para obter informações sobre a estrutura de uma cadeia de caracteres de mensagem e o uso de parâmetros na cadeia de caracteres, consulte a descrição do argumento *msg_str* em [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 É um valor de parâmetro para uso na mensagem. Pode ser mais de um valor de parâmetro. Os valores devem ser especificados na ordem em que as variáveis de espaço reservado aparecem na mensagem. O número máximo de valores é 20.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 Da mesma forma que a instrução RAISERROR, FORMATMESSAGE edita a mensagem substituindo os valores de parâmetros fornecidos nas variáveis de espaço reservado da mensagem. Para obter mais informações sobre os espaços reservados permitidos em mensagens de erro e o processo de edição, consulte [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE pesquisa a mensagem no idioma atual do usuário. Para mensagens do sistema (*msg_number* < = 50000), se não houver versão localizada da mensagem, a versão do idioma do sistema operacional será usada. Para mensagens do usuário (*msg_number* > 50000), se não houver versão localizada da mensagem, a versão em inglês será usada.
  
 Para mensagens localizadas, os valores dos parâmetros fornecidos precisam corresponder aos espaços reservados dos parâmetros na versão em inglês dos EUA. Ou seja, o parâmetro 1 na versão localizada precisa corresponder ao parâmetro 1 na versão em inglês dos EUA, o parâmetro 2 precisa corresponder ao parâmetro 2 e assim por diante.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-example-with-a-message-number"></a>a. Exemplo com um número de mensagem  
 O exemplo a seguir usa uma mensagem de replicação `20009` armazenada em sys.messages como "Não foi possível adicionar o artigo '%s' à publicação '%s'". FORMATMESSAGE substitui os valores `First Variable` e `Second Variable` para os espaços reservados de parâmetro. A cadeia de caracteres resultante, "Não foi possível adicionar o artigo 'First Variable' à publicação 'Second Variable'", é armazenada na variável local `@var1`.  
  
```sql
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. Exemplo com uma cadeia de caracteres de mensagem  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 O exemplo a seguir usa uma cadeia de caracteres como entrada.  
  
```sql
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 Retorna: `This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. Exemplos adicionais de formatação da cadeia de caracteres de mensagem  
 Os exemplos a seguir mostram uma variedade de opções de formatação.  
  
```sql
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);
SELECT FORMATMESSAGE('Signed int with up to 3 leading zeros %03i', 5);  
SELECT FORMATMESSAGE('Signed int with up to 20 leading zeros %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Bigint %I64d', 3000000000);
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
  
  
