---
title: TEXTPTR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfca4f9367a15cf5c418b8d671ae968260323898
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948499"
---
# <a name="text-and-image-functions---textptr-transact-sql"></a>Funções Text e Image – TEXTPTR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor do ponteiro de texto correspondente a uma coluna **text**, **ntext** ou **image** em um formato **varbinary**. O valor do ponteiro de texto recuperado pode ser usado nas instruções READTEXT, WRITETEXT e UPDATETEXT.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] A funcionalidade alternativa não está disponível.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column*  
 É a coluna **text**, **ntext** ou **image** que será usada.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varbinary**  
  
## <a name="remarks"></a>Remarks  
 Para tabelas com texto em linha, TEXTPTR retorna um identificador para que o texto seja processado. É possível obter um ponteiro de texto válido mesmo que o valor de texto seja nulo.  
  
 Não é possível usar a função TEXTPTR em colunas de exibições. Ela só pode ser usada em colunas de tabelas. Para usar a função TEXTPTR em uma coluna de uma exibição, é necessário definir o nível de compatibilidade como 80 usando [Nível de compatibilidade ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Se a tabela não tiver um texto em linha, e se uma coluna **text**, **ntext** ou **image** não foi inicializada por uma instrução UPDATETEXT, TEXTPTR retornará um ponteiro nulo.  
  
 Use TEXTVALID para testar se um ponteiro de texto existe. Não é possível usar UPDATETEXT, WRITETEXT ou READTEXT sem um ponteiro de texto válido.  
  
 Essas funções e instruções também são úteis quando você trabalha com os dados **text**, **ntext** e **image**.  
  
|Função ou instrução|Descrição|  
|---------------------------|-----------------|  
|PATINDEX<b>('</b> _%pattern%_ **' ,** _expression_ **)**|Retorna a posição de caracteres de uma cadeia de caracteres especificada nas colunas **text** ou **ntext**.|  
|DATALENGTH<b>(</b>_expression_ **)**|Retorna o comprimento dos dados nas colunas **text**, **ntext** e **image**.|  
|SET TEXTSIZE|Retorna o limite, em bytes, dos dados **text**, **ntext** ou **image** a serem retornados com uma instrução SELECT.|  
|SUBSTRING<b>(</b>_text_column_, _start_, _length_ **)**|Retorna uma cadeia de caracteres **varchar** especificada pelo deslocamento *start* e o *length* especificados. O comprimento deve ser menor que 8 KB.|  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]  
>  Para executar os exemplos a seguir, é necessário instalar o banco de dados **pubs**.  
  
### <a name="a-using-textptr"></a>A. Usando TEXTPTR  
 O exemplo a seguir usa a função `TEXTPTR` para localizar a coluna **image** `logo` associada a `New Moon Books` na tabela `pub_info` do banco de dados `pubs`. O ponteiro de texto é colocado em uma variável local `@ptrval.`  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. Usando TEXTPTR com texto em linha  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o ponteiro de texto em linha deve ser usado dentro de uma transação, como mostra o exemplo a seguir.  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. Retornando dados de texto  
 O exemplo a seguir seleciona a coluna `pub_id` e o ponteiro de texto de 16 bytes da coluna `pr_info` na tabela `pub_info`.  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 O exemplo a seguir mostra como retornar os primeiros `8000` bytes de texto sem usar TEXTPTR.  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. Retornando dados de texto específicos  
 O exemplo a seguir localiza a coluna `text` (`pr_info`) associada a `pub_id``0736` na tabela `pub_info`do banco de dados `pubs`. Primeiro, ele declara a variável local `@val`. O ponteiro de texto (uma longa cadeia de caracteres binários) é colocado em `@val` e fornecido como parâmetro para a instrução `READTEXT`. Isto retorna 10 bytes, iniciando no quinto byte (deslocamento de 4).  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Funções de texto e imagem &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
