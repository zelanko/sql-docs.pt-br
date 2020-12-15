---
description: sys.fulltext_languages (Transact-SQL)
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e8c29c32323c2c75e573e8e76851e4026a6e815
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464687"
---
# <a name="sysfulltext_languages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Esta exibição do catálogo contém uma linha por idioma cujos separadores de palavras estão registrados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada linha exibe o LCID e o nome do idioma. Quando os separadores de palavras são registrados para um idioma, seus outros recursos lingüísticos, palavras irrelevantes (palavras de ruído) e arquivos de dicionário de sinônimos, ficam disponíveis para operações de indexação/consulta de texto completo. O valor de **Name** ou **LCID** pode ser especificado nas instruções consultas de texto completo e índice de texto completo [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
   
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|**lcid**|**int**|O LCID (identificador de localidade) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows relativo ao idioma.|  
|**name**|**sysname**|É o valor do alias em [sys.sysidiomas](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) correspondentes ao valor de **LCID** ou à representação de cadeia de caracteres do LCID numérico.|  
  
## <a name="values-returned-for-default-languages"></a>Valores retornados para idiomas padrão  
 A tabela a seguir mostra valores para idiomas cujos separadores de palavras são registrados por padrão.  
  
|Idioma|LCID|  
|--------------|----------|  
|Árabe|1025|  
|Bengali (India)|1093|  
|British English|2057|  
|Búlgaro|1026|  
|Catalão|1027|  
|Chinês (RAE de Hong Kong, RPC)|3076|  
|Chinese (Macao SAR)|5124|  
|Chinês (Singapura)|4100|  
|Croata|1.050|  
|Tcheco|1029|  
|Dinamarquês|1030|  
|Holandês|1043|  
|Inglês|1046|  
|Francês|1036|  
|Alemão|1031|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Grego|1032|  
|Guzerate|1095|  
|Hebraico|1037|  
|Híndi|1081|  
|Islandês|1039|  
|Indonésio|1057|  
|Italiano|1040|  
|Japonês|1041|  
|canarim|1099|  
|Coreano|1042|  
|Letão|1062|  
|Lituano|1063|  
|Malay - Malaysia|1086|  
|Malaiala|1100|  
|Marati|1102|  
|Neutro|0|  
|Norueguês (Bokmål)|1044|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Polonês|1045|  
|Português (Brasil)|1046|  
|Português (Portugal)|2070|  
|Panjabi|1094|  
|Romeno|1048|  
|Russo|1049|  
|Sérvio (cirílico)|3098|  
|Sérvio (latino)|2074|  
|Chinês simplificado|2052|  
|Eslovaco|1051|  
|Esloveno|1060|  
|Espanhol|3082|  
|Sueco|1053|  
|Tâmil|1097|  
|Télugo|1098|  
|Tailandês|1054|  
|Chinês tradicional|1028|  
|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Turco|1055|  
|Ucraniano|1058|  
|Urdu|1056|  
|Vietnamita|1066|  
  
## <a name="remarks"></a>Comentários  
 Para atualizar a lista de idiomas registrados com a pesquisa de texto completo, use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_fulltext_load_thesaurus_file ](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar arquivos de dicionário de sinônimos para Full-Text pesquisa](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
