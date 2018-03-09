---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c1659dfcc9ca8908ce756eb41b32fd30649decfa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Lê **texto**, **ntext**, ou **imagem** valores de um **texto**, **ntext**, ou **imagem**  coluna, começando em um deslocamento especificado e o número especificado de bytes de leitura.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use o [subcadeia de caracteres](../../t-sql/functions/substring-transact-sql.md) function em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table* **.** *column*  
 É o nome de uma tabela e uma coluna a partir das quais a leitura será feita. Nomes de tabela e coluna devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação dos nomes de tabela e coluna é necessária; entretanto, a especificação do nome do banco de dados e de nomes de proprietário é opcional.  
  
 *text_ptr*  
 É um ponteiro de texto válido. *text_ptr* devem ser **binário (16)**.  
  
 *offset*  
 É o número de bytes (quando o **texto** ou **imagem** tipos de dados são usados) ou caracteres (quando o **ntext** tipo de dados é usado) para ignorar antes de começar a ler o **texto**, **imagem**, ou **ntext** dados.  
  
 *size*  
 É o número de bytes (quando o **texto** ou **imagem** tipos de dados são usados) ou caracteres (quando o **ntext** tipo de dados é usado) de dados a serem lidos. Se *tamanho* é 0, 4 KB bytes de dados é lida.  
  
 HOLDLOCK  
 Faz com que o valor de texto seja bloqueado para leituras até o final da transação. Outros usuários podem ler o valor, mas não podem modificá-lo.  
  
## <a name="remarks"></a>Remarks  
 Use o [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) função para obter um válido *text_ptr* valor. TEXTPTR retorna um ponteiro para o **texto**, **ntext**, ou **imagem** coluna da linha especificada ou para o **texto**, **ntext** , ou **imagem** coluna na última linha retornada pela consulta se mais de uma linha é retornada. Como TEXTPTR retorna uma cadeia binária de 16 bytes, recomenda-se declarar uma variável local para conter o ponteiro de texto e usá-la com READTEXT. Para obter mais informações sobre como declarar uma variável local, consulte [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podem existir ponteiros de texto em linha, mas podem não ser válidos. Para obter mais informações sobre o **texto em linha** opção, consulte [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter mais informações sobre como invalidar ponteiros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 O valor de @@TEXTSIZE função substitui o tamanho especificado para READTEXT se ele for menor que o tamanho especificado para READTEXT. O @@TEXTSIZE função especifica o limite no número de bytes de dados a serem retornados, definido pela instrução SET TEXTSIZE. Para obter mais informações sobre como definir a configuração de sessão para TEXTSIZE, consulte [SET TEXTSIZE &#40; Transact-SQL &#41; ](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 As permissões de READTEXT usam como padrão os usuários que têm permissões SELECT na tabela especificada. As permissões são transferíveis quando são transferidas permissões SELECT.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lê do segundo até o vigésimo sexto caracteres da coluna `pr_info` na tabela `pub_info`.  
  
> [!NOTE]  
>  Para executar este exemplo, você deve instalar o **pubs** banco de dados de exemplo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
