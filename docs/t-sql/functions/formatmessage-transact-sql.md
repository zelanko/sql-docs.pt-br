---
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c9048efd86a7a4a993a9fff6bcab7f9058144f7e
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843762"
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Constrói uma mensagem com base em uma mensagem existente em sys.messages ou em uma cadeia de caracteres fornecida. A funcionalidade de FORMATMESSAGE se assemelha à da instrução RAISERROR. Entretanto, RAISERROR imprime a mensagem imediatamente, enquanto FORMATMESSAGE retorna a mensagem formatada para processamento posterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_number*  
 É a ID da mensagem armazenada em sys.messages. Se *msg_number* for <= 13.000 ou se a mensagem não existir em sys.messages, NULL será retornado.  
  
 *msg_string*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 É uma cadeia de caracteres entre aspas simples e que contém espaços reservados de valor do parâmetro. A mensagem de erro pode ter no máximo 2.047 caracteres. Se a mensagem tiver 2.048 caracteres ou mais, somente os primeiros 2.044 serão exibidos e um sinal de reticências será adicionado para indicar que a mensagem foi truncada. Observe que os parâmetros de substituição consomem mais caracteres que a saída mostra por causa de comportamento de armazenamento interno.  Para obter informações sobre a estrutura de uma cadeia de caracteres de mensagem e o uso de parâmetros na cadeia de caracteres, consulte a descrição do argumento *msg_str* em [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 É um valor de parâmetro para uso na mensagem. Pode ser mais de um valor de parâmetro. Os valores devem ser especificados na ordem em que as variáveis de espaço reservado aparecem na mensagem. O número máximo de valores é 20.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 Da mesma forma que a instrução RAISERROR, FORMATMESSAGE edita a mensagem substituindo os valores de parâmetros fornecidos nas variáveis de espaço reservado da mensagem. Para obter mais informações sobre os espaços reservados permitidos em mensagens de erro e o processo de edição, consulte [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE pesquisa a mensagem no idioma atual do usuário. Se não houver nenhuma versão localizada da mensagem, a versão em inglês dos EUA será usada.  
  
 Para mensagens localizadas, os valores dos parâmetros fornecidos precisam corresponder aos espaços reservados dos parâmetros na versão em inglês dos EUA. Ou seja, o parâmetro 1 na versão localizada precisa corresponder ao parâmetro 1 na versão em inglês dos EUA, o parâmetro 2 precisa corresponder ao parâmetro 2 e assim por diante.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-example-with-a-message-number"></a>A. Exemplo com um número de mensagem  
 O exemplo a seguir usa uma mensagem de replicação `20009` armazenada em sys.messages como "Não foi possível adicionar o artigo '%s' à publicação '%s'". FORMATMESSAGE substitui os valores `First Variable` e `Second Variable` para os espaços reservados de parâmetro. A cadeia de caracteres resultante, "Não foi possível adicionar o artigo 'First Variable' à publicação 'Second Variable'", é armazenada na variável local `@var1`.  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. Exemplo com uma cadeia de caracteres de mensagem  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 O exemplo a seguir usa uma cadeia de caracteres como entrada.  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 Retorna: `This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. Exemplos adicionais de formatação da cadeia de caracteres de mensagem  
 Os exemplos a seguir mostram uma variedade de opções de formatação.  
  
```  
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
  
  
