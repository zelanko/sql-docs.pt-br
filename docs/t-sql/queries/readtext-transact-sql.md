---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dd8ad58e96956e1ab0f7b542bab4168272b3f968
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141289"
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Lê os valores **text**, **ntext** ou **image** de uma coluna **text**, **ntext** ou **image**. Começa lendo de um deslocamento especificado e lendo o número especificado de bytes.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use a função [SUBSTRING](../../t-sql/functions/substring-transact-sql.md) nesse caso.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumentos  
_table_ **.** _column_  
É o nome de uma tabela e uma coluna a partir das quais a leitura será feita. Os nomes de tabela e de coluna precisam cumprir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação dos nomes de tabela e coluna é necessária; entretanto, a especificação do nome do banco de dados e de nomes de proprietário é opcional.  
  
_text\_ptr_  
É um ponteiro de texto válido. _text\_ptr_ deve ser **binary(16)** .  
  
_offset_  
É o número de bytes quando os tipos de dados **text** ou **image** são usados. Também pode ser o número de bytes para quando o tipo de dados **ntext** for usado para ignorar antes de iniciar a leitura dos dados de **text**, **image** ou **ntext**.  
  
_size_ É o número de bytes quando os tipos de dados **text** ou **image** são usados. Ele também pode ser o número de bytes para caracteres quando o tipo de dados **ntext** é usado para os dados serem lidos. Se _size_ for 0, 4 KB de dados serão lidos.  
  
HOLDLOCK  
Faz com que o valor de texto seja bloqueado para leituras até o final da transação. Outros usuários podem ler o valor, mas não podem modificá-lo.  
  
## <a name="remarks"></a>Remarks  
Use a função [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) para obter um valor de _text\_ptr_ válido. TEXTPTR retorna um ponteiro para as colunas **text**, **ntext** ou **image** na linha especificada. TEXTPRT também pode retornar um ponteiro ou para as colunas **text**, **ntext** ou **image** na última linha que a consulta retorna caso a consulta retorne mais de uma linha. Como TEXTPTR retorna uma cadeia binária de 16 bytes, recomenda-se declarar uma variável local para conter o ponteiro de texto e usá-la com READTEXT. Para obter mais informações de como declarar uma variável local, confira [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podem existir ponteiros de texto em linha, mas podem não ser válidos. Para obter mais informações sobre a opção **text in row**, confira [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter mais informações de como invalidar ponteiros de texto, confira [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
O valor da função @@TEXTSIZE substituirá o tamanho especificado para READTEXT se for menor que o tamanho especificado para READTEXT. A função @@TEXTSIZE especifica o limite do número de bytes de dados a serem retornados, definido pela instrução SET TEXTSIZE. Para obter mais informações de como definir a configuração de sessão para TEXTSIZE, confira [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
As permissões de READTEXT usam como padrão os usuários que têm permissões SELECT na tabela especificada. As permissões são transferíveis quando são transferidas permissões SELECT.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir lê do segundo até o vigésimo sexto caractere da coluna `pr_info` na tabela `pub_info`.  
  
> [!NOTE]  
>  Para executar este exemplo, você precisa instalar o banco de dados **pubs** de exemplo.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
