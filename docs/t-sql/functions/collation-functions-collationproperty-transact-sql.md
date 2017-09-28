---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94cbf96a25a84af1eddce9d94555be9c558c3470
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funções de agrupamento - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna a propriedade de um agrupamento especificado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*collation_name*  
É o nome do agrupamento. *collation_name* é **nvarchar (128)**, sem padrão.
  
*propriedade*  
É a propriedade do agrupamento. *propriedade* é **varchar (128)**, e pode ser qualquer um dos seguintes valores:
  
|Nome da propriedade|Description|  
|---|---|
|**CodePage**|Página de código de não Unicode do agrupamento.|  
|**LCID**|Windows LCID do agrupamento.|  
|**ComparisonStyle**|Estilo de comparação do agrupamento do Windows. Retorna 0 para todos os agrupamentos binários.|  
|**Versão**|A versão do agrupamento, extraída do campo de versão da identificação do agrupamento. Retorna 2, 1 ou 0.<br /><br /> Agrupamentos com "100" no nome) retornam 2.<br /><br /> Agrupamentos com "90" no nome) retorne 1.<br /><br /> Todos os outros agrupamentos retornam 0.|  
  
## <a name="return-types"></a>Tipos de retorno
**sql_variant**
  
## <a name="examples"></a>Exemplos  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Consulte também
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  


