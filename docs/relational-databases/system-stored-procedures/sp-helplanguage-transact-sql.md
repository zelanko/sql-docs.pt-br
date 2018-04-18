---
title: sp_helplanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5447f5cb5f41ab4c9a2dfa162e6ee04932c515c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Relata informações sobre um idioma alternativo específico ou sobre todos os idiomas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@language=** ] **'***idioma***'**  
 É o nome do idioma alternativo para o qual exibir informações. *idioma* é **sysname**, com um padrão NULL. Se *idioma* for especificado, serão retornadas informações sobre o idioma especificado. Se o idioma não for especificado, informações sobre todos os idiomas no **sys. syslanguages** exibição de compatibilidade é retornada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|Número de identificação do idioma.|  
|**dateformat**|**nchar(3)**|Formato da data.|  
|**DATEFIRST**|**tinyint**|Primeiro dia da semana: 1 para segunda-feira, 2 para terça-feira e assim por diante, até 7 para domingo.|  
|**Atualizar**|**Int**|Versão da última atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este idioma.|  
|**name**|**sysname**|Nome do idioma.|  
|**alias**|**sysname**|Nome alternativo do idioma.|  
|**Meses**|**nvarchar(372)**|Nomes de meses.|  
|**shortmonths**|**nvarchar(132)**|Nomes abreviados de meses.|  
|**Dias**|**nvarchar(217)**|Nomes de dias.|  
|**lcid**|**Int**|ID de localidade do Windows para o idioma.|  
|**msglangid**|**smallint**|ID do grupo de mensagens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-a-single-language"></a>A. Retornando informações sobre um único idioma  
 O exemplo a seguir exibe informações sobre o idioma alternativo `French`.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. Retornando informações sobre todos os idiomas  
 O exemplo a seguir exibe informações sobre todos os idiomas alternativos instalados.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
