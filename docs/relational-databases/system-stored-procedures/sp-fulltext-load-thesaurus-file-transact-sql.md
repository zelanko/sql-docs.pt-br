---
title: sp_fulltext_load_thesaurus_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2449a78012f50b6a785fdaef6cd8a9b2785f40ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spfulltextloadthesaurusfile-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Faz com que a instância do servidor analise e carregue os dados do arquivo do dicionário de sinônimos que corresponde ao idioma cujo LCID está especificado. Esse procedimento armazenado é útil após a atualização de um arquivo de dicionário de sinônimos. Executar **sp_fulltext_load_thesaurus_file** provoca a recompilação de consultas de texto completo que usam o dicionário de sinônimos do LCID especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *lcid*  
 Inteiro que mapeia o identificador de localidade (LCID) da linguagem para a qual você quer carregar a definição XML do dicionário de sinônimos. Para obter o LCIDs de idiomas que estão disponíveis em uma instância de servidor, use o [sys. fulltext_languages &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) exibição do catálogo.  
  
 **@loadOnlyIfNotLoaded** = *Ação*  
 Especifica se o arquivo de dicionário de sinônimos é carregado nas tabelas de dicionário de sinônimos mesmo que ele já tenha sido carregado. *ação* é um de:  
  
|Value|Definição|  
|-----------|----------------|  
|**0**|Carrega o arquivo de dicionário de sinônimos independentemente dele já ter sido carregado. Esse é o comportamento padrão de **sp_fulltext_load_thesaurus_file**.|  
|1|Carregar o arquivo de dicionário de sinônimos apenas se ele ainda não tiver sido carregado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Arquivos de dicionários de sinônimos são carregados automaticamente por consultas de texto completo que usam o dicionário de sinônimos. Para evitar esse impacto de desempenho pela primeira vez em consultas de texto completo, é recomendável que você execute **sp_fulltext_load_thesaurus_file**.  
  
 Use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' para atualizar a lista de idiomas registrados na pesquisa de texto completo.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor ou o administrador do sistema pode executar o **sp_fulltext_load_thesaurus_file** procedimento armazenado.  
  
 Somente administradores do sistema podem atualizar, modificar ou excluir arquivos de dicionário de sinônimos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>A. Carregar um arquivo de dicionário de sinônimos mesmo que ele já tenha sido carregado  
 O exemplo a seguir analisa e carrega o dicionário de sinônimos em inglês.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
GO  
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. Carregar um arquivo de dicionário de sinônimos apenas se ele ainda não tiver sido carregado  
 O exemplo a seguir analisa e carrega o arquivo de dicionário de sinônimos em árabe, a não ser que já tenha sido carregado.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
  
