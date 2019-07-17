---
title: sp_helplanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d46e178fc1872a84bb573f16629803c59f2fb6c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122506"
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
`[ @language = ] 'language'` É o nome do idioma alternativo para o qual exibir informações. *linguagem* está **sysname**, com um padrão NULL. Se *linguagem* for especificado, serão retornadas informações sobre o idioma especificado. Se o idioma não for especificado, informações sobre todos os idiomas na **sys. syslanguages** exibição de compatibilidade é retornada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|Número de identificação do idioma.|  
|**dateformat**|**nchar(3)**|Formato da data.|  
|**datefirst**|**tinyint**|Primeiro dia da semana: 1 para segunda-feira, 2 para terça-feira, e assim por diante, até 7 para domingo.|  
|**Atualizar**|**int**|Versão da última atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este idioma.|  
|**name**|**sysname**|Nome do idioma.|  
|**alias**|**sysname**|Nome alternativo do idioma.|  
|**meses**|**nvarchar(372)**|Nomes de meses.|  
|**shortmonths**|**nvarchar(132)**|Nomes abreviados de meses.|  
|**Dias**|**nvarchar(217)**|Nomes de dias.|  
|**lcid**|**int**|ID de localidade do Windows para o idioma.|  
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
  
  
