---
title: ALTER FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fb0a6c02a3211c029c311f07a91da9b26842fc4f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666134"
---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Insere ou exclui uma palavra irrelevante na lista de palavras irrelevantes de texto completo padrão do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 É o nome da lista de palavras irrelevantes que está sendo alterada. *stoplist_name* pode ter, no máximo, 128 caracteres.  
  
 **'** *stopword* **'**  
 É uma cadeia de caracteres que pode ser uma palavra com significado linguístico no idioma especificado ou um token sem significado linguístico. *stopword* é limitado ao tamanho máximo do token (64 caracteres). Uma palavra irrelevante pode ser especificada como uma cadeia de caracteres de Unicode.  
  
 LANGUAGE *language_term*  
 Especifica o idioma a ser associado à *stopword* que está sendo adicionada ou removida.  
  
 *language_term* pode ser especificado como uma cadeia de caracteres, um inteiro ou valor hexadecimal que corresponde ao LCID (ID de localidade) do idioma, da seguinte maneira:  
  
|Formato|Descrição|  
|------------|-----------------|  
|Cadeia de caracteres|*language_term* corresponde ao valor da coluna **alias** no modo de exibição de compatibilidade [sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). A cadeia de caracteres precisa ser colocada entre aspas, como em **'***language_term***'**.|  
|Integer|*language_term* é o LCID do idioma.|  
|Hexadecimal|*language_term* é 0x seguido do valor hexadecimal do LCID. O valor hexadecimal não deve exceder oito dígitos, inclusive zeros à esquerda. Se o valor estiver no formato DBCS (conjunto de caracteres de dois bytes), o SQL Server o converterá em Unicode.|  
  
 ADD **'***stopword***'** LANGUAGE *language_term*  
 Adiciona uma palavra irrelevante à lista de palavras irrelevantes do idioma especificado por LANGUAGE *language_term*.  
  
 Se a combinação especificada de palavra-chave e o valor LCID do idioma não forem exclusivos da STOPLIST, um erro será retornado.  Se o valor LCID não corresponder a um idioma registrado, um erro será gerado.  
  
 DROP { **'***stopword***'** LANGUAGE *language_term* | ALL LANGUAGE *language_term* | ALL }  
 Descarta uma palavra irrelevante da lista de palavras irrelevantes.  
  
 **'** *stopword* **'** LANGUAGE *language_term*  
 Remove a palavra irrelevante especificada para o idioma especificado por *language_term*.  
  
 ALL LANGUAGE *language_term*  
 Remove todas as palavras irrelevantes para o idioma especificado por *language_term*.  
  
 ALL  
 Descarta todas as palavras irrelevantes da lista de palavras irrelevantes.  
  
## <a name="remarks"></a>Remarks  
 Só há suporte para CREATE FULLTEXT STOPLIST no nível de compatibilidade 100 e superior. Nos níveis de compatibilidade 80 e 90, a lista de palavras irrelevantes do sistema sempre é atribuída ao banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Para designar uma lista de palavras irrelevantes como a lista de palavras irrelevantes padrão do banco de dados é necessário ter a permissão ALTER DATABASE. Para, de outro modo, alterar uma lista de palavras irrelevantes, é necessário ser o proprietário da lista de palavras irrelevantes ou ter a associação às funções de banco de dados fixas **db_owner** ou **db_ddladmin**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera uma lista de palavras irrelevantes chamada `CombinedFunctionWordList`, adicionando a palavra 'en', primeiro para espanhol e depois para francês.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
