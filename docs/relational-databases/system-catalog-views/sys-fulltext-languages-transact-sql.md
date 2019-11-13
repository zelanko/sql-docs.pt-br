---
title: sys.fulltext_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e5af224150508f048d91345cba595517209f824d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981772"
---
# <a name="sysfulltext_languages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por idioma cujos separadores de palavras estão registrados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha exibe o LCID e o nome do idioma. Quando os separadores de palavras são registrados para um idioma, seus outros recursos lingüísticos, palavras irrelevantes (palavras de ruído) e arquivos de dicionário de sinônimos, ficam disponíveis para operações de indexação/consulta de texto completo. O valor de **Name** ou **LCID** pode ser especificado nas instruções consultas de texto completo e [!INCLUDE[tsql](../../includes/tsql-md.md)] de índice de texto completo.  
   
|Column|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|**lcid**|**int**|O LCID (identificador de localidade) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows relativo ao idioma.|  
|**name**|**sysname**|É o valor do alias em [Sys. syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) correspondente ao valor de **LCID** ou à representação de cadeia de caracteres do LCID numérico.|  
  
## <a name="values-returned-for-default-languages"></a>Valores retornados para idiomas padrão  
 A tabela a seguir mostra valores para idiomas cujos separadores de palavras são registrados por padrão.  
  
|Language|LCID|  
|--------------|----------|  
|Arabic|1025|  
|Bengali (India)|1093|  
|British English|2057|  
|Bulgarian|1026|  
|Catalan|1027|  
|Chinês (RAE de Hong Kong, RPC)|3076|  
|Chinese (Macao SAR)|5124|  
|Chinês (Singapura)|4100|  
|Croatian|1050|  
|Czech|1029|  
|Dinamarquês|1030|  
|Dutch|1043|  
|English|1046|  
|French|1036|  
|German|1031|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Greek|1032|  
|Gujarati|1095|  
|Hebrew|1037|  
|Hindi|1081|  
|Icelandic|1039|  
|Indonesian|1057|  
|Italian|1040|  
|Japanese|1041|  
|canarim|1099|  
|Korean|1042|  
|Latvian|1062|  
|Lithuanian|1063|  
|Malay - Malaysia|1086|  
|Malayalam|1100|  
|Marathi|1102|  
|Neutral|0|  
|Norwegian (Bokmål)|1044|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Polish|1045|  
|Portuguese (Brazil)|1046|  
|Portuguese (Portugal)|2070|  
|Punjabi|1094|  
|Romanian|1048|  
|Russian|1049|  
|Serbian (Cyrillic)|3098|  
|Serbian (Latin)|2074|  
|Simplified Chinese|2052|  
|Slovak|1051|  
|Slovenian|1060|  
|Spanish|3082|  
|Swedish|1053|  
|Tamil|1097|  
|Telugu|1098|  
|Thai|1054|  
|Traditional Chinese|1028|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Turkish|1055|  
|Ukrainian|1058|  
|Urdu|1056|  
|Vietnamese|1066|  
  
## <a name="remarks"></a>Remarks  
 Para atualizar a lista de idiomas registrados com a pesquisa de texto completo, use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
