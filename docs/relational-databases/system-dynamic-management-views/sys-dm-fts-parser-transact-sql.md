---
title: sys. dm_fts_parser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_parser_TSQL
- dm_fts_parser
- dm_fts_parser_TSQL
- sys.dm_fts_parser
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_parser dynamic management function
- troubleshooting [SQL Server], full-text search
ms.assetid: 2736d376-fb9d-4b28-93ef-472b7a27623a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: fa60c1785e0740dde4bc6b3755dea36db8a5a21a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900914"
---
# <a name="sysdm_fts_parser-transact-sql"></a>sys.dm_fts_parser (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o resultado final de geração de tokens após a aplicação de uma determinada combinação de separador de [palavras](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md), [dicionário de sinônimos](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)e [parada](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) de uma cadeia de caracteres de consulta. O resultado da geração de tokens é equivalente à saída do Mecanismo de Texto Completo para a cadeia de caracteres de consulta especificada.  
  
 sys.dm_fts_parser é uma função de gerenciamento dinâmico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_fts_parser('query_string', lcid, stoplist_id, accent_sensitivity)  
```  
  
## <a name="arguments"></a>Argumentos  
 *query_string*  
 A consulta que você deseja analisar. *QUERY_STRING* pode ser uma cadeia de cadeia de caracteres que [contém](../../t-sql/queries/contains-transact-sql.md) suporte à sintaxe. Por exemplo, é possível incluir formas flexionadas, uma dicionário de sinônimo e operadores lógicos.  
  
 *LCID*  
 LCID (identificador de localidade) do separador de palavras a ser usado para a análise de *QUERY_STRING*.  
  
 *stoplist_id*  
 ID da STOPLIST, se houver, a ser usada pelo separador de palavras identificado por *LCID*. *stoplist_id* é **int**. Se você especificar ' NULL ', nenhumalist de parada será usada. Se especificar 0, será usada a LISTA DE PALAVRAS IRRELEVANTES do sistema.  
  
 Uma ID da lista de palavras irrelevantes é exclusiva em um banco de dados. Para obter a ID de STOPLIST para um índice de texto completo em uma determinada tabela, use a exibição de catálogo [Sys. fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) .  
  
 *accent_sensitivity*  
 Valor Booliano que controla se a pesquisa de texto completo diferencia ou não diacríticos. *accent_sensitivity* é **bit**, com um dos seguintes valores:  
  
|Valor|A distinção de acentos é...|  
|-----------|----------------------------|  
|0|Não diferencia<br /><br /> Palavras como "café" e "cafe" são tratadas da mesma forma.|  
|1|Sigiloso<br /><br /> Palavras como "café" e "cafe" são tratadas de forma diferente.|  
  
> [!NOTE]  
>  Para exibir a configuração atual desse valor para um catálogo de texto completo, [!INCLUDE[tsql](../../includes/tsql-md.md)] execute a seguinte instrução: `SELECT fulltextcatalogproperty('` *catalog_name*`', 'AccentSensitivity');`.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|palavra-chave|**varbinary(128)**|A representação hexadecimal de uma determinada palavra-chave retornada por um separador de palavras. Essa representação é usada para armazenar a palavra-chave no índice de texto completo. Esse valor não é legível, mas é útil para relacionar uma determinada palavra-chave à saída retornada por outras exibições de gerenciamento dinâmico que retornam o conteúdo de um índice de texto completo, como [Sys. dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md) e [Sys. dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md).<br /><br /> **Observação:** OxFF representa o caractere especial que indica o fim de um arquivo ou conjunto de um DataSet.|  
|group_id|**int**|Contém um valor de inteiro que é útil para diferenciar o grupo lógico a partir do qual um determinado termo foi gerado. Por exemplo, '`Server AND DB OR FORMSOF(THESAURUS, DB)"`' produz os seguintes valores group_id em inglês:<br /><br /> 1: servidor<br />2: BD<br />3: BD|  
|phrase_id|**int**|Contém um valor inteiro que é útil para diferenciar os casos em que formas alternativas de palavras compostas, como texto completo, são geradas pelo separador de palavras. Às vezes, devido à existência de palavras compostas ('multi-million'), formas alternativas são geradas pelo separador de palavras. Às vezes, essas formas alternativas (frases) precisam ser diferenciadas.<br /><br /> Por exemplo, '`multi-million`' produz os seguintes valores phrase_id em inglês:<br /><br /> 1 para`multi`<br />1 para`million`<br />2 para`multimillion`|  
|ocorrência|**int**|Indica a ordem de cada termo no resultado da análise. Por exemplo, a ocorrência "`SQL Server query processor`" de frase poderia conter os seguintes valores de ocorrência para os termos da frase em inglês:<br /><br /> 1 para`SQL`<br />2 para`Server`<br />3 para`query`<br />4 para`processor`|  
|special_term|**nvarchar(4000)**|Contém informações sobre as características do termo que está sendo emitido pelo separador de palavras, um destes:<br /><br /> Correspondência exata<br /><br /> Palavra de ruído<br /><br /> Fim de oração<br /><br /> Fim de parágrafo<br /><br /> Fim de capítulo|  
|display_term|**nvarchar(4000)**|Contém a forma legível da palavra-chave. Como ocorre com as funções criadas para acessar o conteúdo do índice de texto completo, esse termo exibido pode não ser idêntico ao termo original por motivo de limitação de desnormalização. No entanto, ele precisar ser preciso o suficiente para ajudar você a identificá-lo da entrada original.|  
|expansion_type|**int**|Contém informações sobre a natureza da expansão de um determinado termo, um destes:<br /><br /> 0 = Palavra única<br /><br /> 2 = Expansão flexional<br /><br /> 4 = Expansão/substituição do dicionário de sinônimos<br /><br /> Por exemplo, considere um caso no qual o dicionário de sinônimos define a execução como uma expansão de `jog`:<br /><br /> `<expansion>`<br /><br /> `<sub>run</sub>`<br /><br /> `<sub>jog</sub>`<br /><br /> `</expansion>`<br /><br /> O termo `FORMSOF (FREETEXT, run)` gera a seguinte saída:<br /><br /> 
  `run` com expansion_type=0<br /><br /> 
  `runs` com expansion_type=2<br /><br /> 
  `running` com expansion_type=2<br /><br /> 
  `ran` com expansion_type=2<br /><br /> 
  `jog` com expansion_type=4|  
|source_term|**nvarchar(4000)**|O termo ou frase a partir do qual um determinado termo foi gerado ou analisado. Por exemplo, uma consulta no "'`word breakers" AND stemmers'` produz os seguintes valores source_term em inglês:<br /><br /> `word breakers`para o display_term`word`<br />`word breakers`para o display_term`breakers`<br />`stemmers`para o display_term`stemmers`|  
  
## <a name="remarks"></a>Comentários  
 **Sys. dm_fts_parser** dá suporte à sintaxe e aos recursos de predicados de texto completo, como [Contains](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md), e funções, como [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md).  
  
## <a name="using-unicode-for-parsing-special-characters"></a>Usando o Unicode para analisar caracteres especiais  
 Quando você analisa uma cadeia de caracteres de consulta, **Sys. dm_fts_parser** usa o agrupamento do banco de dados ao qual você está conectado, a menos que você especifique a cadeia de caracteres de consulta como Unicode. No entanto, para uma cadeia de caracteres não Unicode que contém caracteres especiais, como ü ou ç, a saída pode ser inesperada, dependendo da ordenação do banco de dados. Para processar uma cadeia de caracteres de consulta independentemente do agrupamento de banco de dados `N`, Prefixe a `N'`cadeia de caracteres com, ou seja, *QUERY_STRING*`'`.  
  
 Para obter mais informações, consulte “C. Exibindo a saída de uma cadeia de caracteres que contém caracteres especiais", posteriormente neste tópico.  
  
## <a name="when-to-use-sysdm_fts_parser"></a>Quando usar sys.dm_fts_parser  
 **Sys. dm_fts_parser** pode ser muito eficiente para fins de depuração. Alguns dos principais cenários de uso incluem:  
  
-   Para entender como um determinado separador de palavras trata uma certa entrada  
  
     Quando uma consulta retorna resultados inesperados, uma causa provável é a maneira como o separador de palavras está analisando e separando os dados. Ao usar sys.dm_fts_parser, você descobre o resultado que um separador de palavras passa para o índice de texto completo. Além disso, você pode consultar quais termos são palavras irrelevantes, que não são pesquisadas no índice de texto completo. Se um termo é um palavra irrelevante para um determinado idioma depende se ele está nalist de palavras irrelevantes especificada pelo valor *stoplist_id* declarado na função.  
  
     Observe também o sinalizador de distinção de acento, que permitirá o usuário ver como o separador de palavras analisará a entrada tendo considerando as informações de distinção de acentos.  
  
-   Para entender como o lematizador funciona em uma determinada entrada  
  
     Você pode saber como o separador de palavras e o lematizador analisam um termo da consulta e suas formas lematizadoras especificando uma consulta CONTAINS ou CONTAINSTABLE contendo a cláusula FORMSOF a seguir:  
  
    ```  
    FORMSOF( INFLECTIONAL, query_term )  
    ```  
  
     Os resultados indicam quais termos estão sendo passados ao índice de texto completo.  
  
-   Para entender como o dicionário de sinônimos expande ou substitui toda a entrada ou parte dela  
  
     Você também pode especificar:  
  
    ```  
    FORMSOF( THESAURUS, query_term )  
    ```  
  
     O resultado dessa consulta mostra como o separador de palavras e o dicionário de sinônimos interagem com relação ao termo da consulta. É possível ver a expansão ou as substituições feitas a partir do dicionário de sinônimos e identificar a consulta resultante que está sendo emitida para o índice de texto completo.  
  
     Observe que se o usuário emitir:  
  
    ```  
    FORMSOF( FREETEXT, query_term )  
    ```  
  
     Os recursos de flexão e de dicionário de sinônimos ocorrerão automaticamente.  
  
 Além dos cenários de uso anteriores, sys.dm_fts_parser pode ajudar consideravelmente a entender e solucionar vários outros problemas relacionados a consultas de texto de completo.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função de servidor fixa **sysadmin** e direitos de acesso àlist de parada especificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-the-output-of-a-given-word-breaker-for-a-keyword-or-phrase"></a>a. Exibindo a saída de um determinado separador de palavras para uma palavra-chave ou frase  
 O exemplo a seguir retorna a saída a partir do uso do separador de palavras em inglês, cujo LCID é 1033, e nenhuma lista de palavras irrelevantes na cadeia de caracteres de consulta a seguir:  
  
 `The Microsoft business analysis`  
  
 A distinção de acentos foi desabilitada.  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis" ', 1033, 0, 0);  
```  
  
### <a name="b-displaying-the-output-of-a-given-word-breaker-in-the-context-of-stoplist-filtering"></a>B. Exibindo a saída de um determinado separador de palavras no contexto de filtro da lista de palavras irrelevantes  
 O exemplo a seguir retorna a saída a partir do uso do separador de palavras em inglês, cujo LCID é 1033, uma lista de palavras irrelevantes em inglês, cuja ID é 77, na cadeia de caracteres de consulta a seguir:  
  
 `"The Microsoft business analysis" OR "MS revenue"`  
  
 A distinção de acentos foi desabilitada.  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis"  OR " MS revenue" ', 1033, 77, 0);  
```  
  
### <a name="c-displaying-the-output-of-a-string-that-contains-special-characters"></a>C. Exibindo a saída de uma cadeia de caracteres que contém caracteres especiais  
 O exemplo a seguir usa o Unicode para analisar a cadeia de caracteres franceses a seguir:  
  
 `français`  
  
 O exemplo especifica o LCID do idioma francês `1036` e a ID de uma lista de palavras irrelevantes definida pelo usuário `5`. A distinção de acentos está habilitada.  
  
```sql
SELECT * FROM sys.dm_fts_parser(N'français', 1036, 5, 1);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)   
 [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Protegíveis](../../relational-databases/security/securables.md)  
  
  
