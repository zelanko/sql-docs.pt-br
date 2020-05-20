---
title: sp_fulltext_load_thesaurus_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ac01c2d29dbe79d0a5702e1bd42730d0b31efcf2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827754"
---
# <a name="sp_fulltext_load_thesaurus_file-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Faz com que a instância do servidor analise e carregue os dados do arquivo do dicionário de sinônimos que corresponde ao idioma cujo LCID está especificado. Esse procedimento armazenado é útil após a atualização de um arquivo de dicionário de sinônimos. A execução de **sp_fulltext_load_thesaurus_file** causa a recompilação de consultas de texto completo que usam o dicionário de sinônimos do LCID especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *lcid*  
 Inteiro que mapeia o identificador de localidade (LCID) da linguagem para a qual você quer carregar a definição XML do dicionário de sinônimos. Para obter os LCIDs de idiomas que estão disponíveis em uma instância de servidor, use a exibição de catálogo [fulltext_languages de&#41;do &#40;do Transact-SQL](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) .  
  
 ** \@ **  =  *ação* loadOnlyIfNotLoaded  
 Especifica se o arquivo de dicionário de sinônimos é carregado nas tabelas de dicionário de sinônimos mesmo que ele já tenha sido carregado. a *ação* é uma de:  
  
|Valor|Definição|  
|-----------|----------------|  
|**0**|Carrega o arquivo de dicionário de sinônimos independentemente dele já ter sido carregado. Esse é o comportamento padrão de **sp_fulltext_load_thesaurus_file**.|  
|1|Carregar o arquivo de dicionário de sinônimos apenas se ele ainda não tiver sido carregado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Não  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Arquivos de dicionários de sinônimos são carregados automaticamente por consultas de texto completo que usam o dicionário de sinônimos. Para evitar esse impacto de desempenho inicial em consultas de texto completo, recomendamos que você execute **sp_fulltext_load_thesaurus_file**.  
  
 Use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' para atualizar a lista de idiomas registrados com a pesquisa de texto completo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou do administrador do sistema podem executar o procedimento armazenado **sp_fulltext_load_thesaurus_file** .  
  
 Somente administradores do sistema podem atualizar, modificar ou excluir arquivos de dicionário de sinônimos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>a. Carregar um arquivo de dicionário de sinônimos mesmo que ele já tenha sido carregado  
 O exemplo a seguir analisa e carrega o dicionário de sinônimos em inglês.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1033;
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. Carregar um arquivo de dicionário de sinônimos apenas se ele ainda não tiver sido carregado  
 O exemplo a seguir analisa e carrega o arquivo de dicionário de sinônimos em árabe, a não ser que já tenha sido carregado.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;
```  

## <a name="see-also"></a>Consulte Também

[FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
[Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
[Configurar e gerenciar arquivos de dicionário de sinônimos para Pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)
