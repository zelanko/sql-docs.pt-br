---
title: FULLTEXTCATALOGPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FULLTEXTCATALOGPROPERTY_TSQL
- FULLTEXTCATALOGPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], properties
- FULLTEXTCATALOGPROPERTY function
- status information [SQL Server], full-text catalogs
ms.assetid: f841dc79-2044-4863-aff0-56b8bb61f250
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 383eafdda02f402d1c398183bfedac6dde85d9ce
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="fulltextcatalogproperty-transact-sql"></a>FULLTEXTCATALOGPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre propriedades de catálogo de texto completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FULLTEXTCATALOGPROPERTY ('catalog_name' ,'property')  
```  
  
## <a name="arguments"></a>Argumentos  
  
> [!NOTE]  
>  As propriedades a seguir serão removidas em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **LogSize** e **PopulateStatus**. Evite usá-las em um novo projeto de desenvolvimento e planeje a modificação dos aplicativos que as utilizam atualmente.  
  
 *catalog_name*  
 É uma expressão que contém o nome do catálogo de texto completo.  
  
 *propriedade*  
 É uma expressão que contém o nome da propriedade do catálogo de texto completo. A tabela lista as propriedades e fornece descrições das informações retornadas.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**AccentSensitivity**|Configuração da diferenciação de caracteres com/sem acento.<br /><br /> 0 = não diferencia caracteres com/sem acento<br /><br /> 1 = diferencia caracteres com/sem acento|  
|**IndexSize**|Tamanho lógico do catálogo de texto completo em MB (megabytes). Inclui o tamanho da frase-chave semântica e índices de semelhança de documento.<br /><br /> Para obter mais informações, consulte "Comentários", mais adiante neste tópico.|  
|**ItemCount**|Número de itens indexados que incluem todo o texto completo, frases-chave e índices de semelhança de documento em um catálogo|  
|**LogSize**|Com suporte somente para compatibilidade com versões anteriores. Sempre retorna 0.<br /><br /> Tamanho, em bytes, do conjunto combinado de logs de erros associado a um catálogo de texto completo do Serviço de Pesquisa do [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**MergeStatus**|Se uma mesclagem mestra está em andamento.<br /><br /> 0 = não há mesclagem mestra em andamento.<br /><br /> 1= há mesclagem mestra em andamento|  
|**PopulateCompletionAge**|A diferença em segundos entre a conclusão da última população do índice de texto completo e 01/01/1990 00:00:00.<br /><br /> Atualizado apenas para rastreamentos completos e incrementais. Retorna 0 caso não haja população.|  
|**PopulateStatus**|0 = Ocioso<br /><br /> 1 = População completa em andamento<br /><br /> 2 = Pausado<br /><br /> 3 = Acelerado<br /><br /> 4 = Recuperando<br /><br /> 5 = Desligado<br /><br /> 6 = População incremental em andamento<br /><br /> 7 = Construindo índice<br /><br /> 8 = O disco está cheio. Em pausa.<br /><br /> 9 = Controle de alterações|  
|**UniqueKeyCount**|Número de chaves exclusivas no catálogo de texto completo.|  
|**ImportStatus**|Se o catálogo de texto completo está sendo importado.<br /><br /> 0= O catálogo de texto completo não está sendo importado.<br /><br /> 1= O catálogo de texto completo está sendo importado.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas emissoras de metadados, como FULLTEXTCATALOGPROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [sp_help_fulltext_catalogs &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 FULLTEXTCATALOGPROPERTY ('*catalog_name*','**IndexSize**') examina apenas os fragmentos com status 4 ou 6 conforme mostrado na [fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md). Estes fragmentos fazem parte do índice lógico. Portanto, o **IndexSize** propriedade retorna apenas o tamanho do índice lógico. Porém, durante uma mesclagem de índice, o tamanho real do índice pode ser o dobro do seu tamanho lógico. Para localizar o tamanho real que está sendo consumido por um índice de texto completo durante uma mesclagem, use o [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) procedimento armazenado do sistema. Esse procedimento analisa todos os fragmentos associados a um índice de texto completo. Se você restringir o crescimento do arquivo de catálogo de texto completo e não permitir espaço suficiente para o processo de mesclagem, a população de texto completo poderá falhar. Nesse caso, FULLTEXTCATALOGPROPERTY ('catalog_name' ,'IndexSize') retorna 0 e o seguinte erro é gravado no log de texto completo:  
  
 `Error: 30059, Severity: 16, State: 1. A fatal error occurred during a full-text population and caused the population to be cancelled. Population type is: FULL; database name is FTS_Test (id: 13); catalog name is t1_cat (id: 5); table name t1 (id: 2105058535). Fix the errors that are logged in the full-text crawl log. Then, resume the population. The basic Transact-SQL syntax for this is: ALTER FULLTEXT INDEX ON table_name RESUME POPULATION.`  
  
 É importante que os aplicativos não esperar em um loop estreito, verificando o **PopulateStatus** propriedade fique ociosa (indicando que a população foi concluída) porque isso leva ciclos da CPU do banco de dados e de texto completo processos de pesquisa e tempos limite de causas. Além disso, geralmente é a melhor opção para verificar o correspondente **PopulateStatus** propriedade no nível de tabela, **TableFullTextPopulateStatus** na função de sistema OBJECTPROPERTYEX. Essa e outras propriedades de texto completo novas em OBJECTPROPERTYEX fornecem informações mais detalhadas sobre as tabelas de indexação de texto completo. Para obter mais informações, veja [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de itens indexados de texto completo de um catálogo de texto completo chamado `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT fulltextcatalogproperty('Cat_Desc', 'ItemCount');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [FULLTEXTSERVICEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
  
  

