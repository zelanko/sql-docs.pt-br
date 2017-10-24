---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 279022316af7e3a396c7089f48933281264f900f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Funções de texto e imagem - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Um **texto**, **ntext**, ou **imagem** função que verifica se um ponteiro de texto específico é válido.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] A funcionalidade alternativa não está disponível.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table*  
 É o nome da tabela que será usada.  
  
 *coluna*  
 É o nome da coluna que será usada.  
  
 *text_ptr*  
 É o ponteiro de texto a ser verificado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 Retorna 1 se o ponteiro for válido e 0 se o ponteiro não for válido. Observe que o identificador para o **texto** coluna deve incluir o nome da tabela. Não é possível usar UPDATETEXT, WRITETEXT ou READTEXT sem um ponteiro de texto válido.  
  
 As instruções e funções a seguir também são úteis quando você trabalha com **texto**, **ntext**, e **imagem** dados.  
  
|Função ou instrução|Description|  
|---------------------------|-----------------|  
|PATINDEX**(**'*padrão %**'***,** *expressão***)**|Retorna a posição do caractere de uma cadeia de caracteres especificada em **texto** e **ntext** colunas.|  
|DATALENGTH**(***expressão***)**|Retorna o comprimento dos dados em **texto**, **ntext**, e **imagem** colunas.|  
|SET TEXTSIZE|Retorna o limite, em bytes, do **texto**, **ntext**, ou **imagem** dados a serem retornados com uma instrução SELECT.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir informa se um ponteiro de texto válido existe para cada valor na coluna `logo` da tabela `pub_info`.  
  
> [!NOTE]  
>  Para executar este exemplo, você deve instalar o **pubs** banco de dados.  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [Definir tamanho do texto &#40; Transact-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Funções de imagem e texto &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  

