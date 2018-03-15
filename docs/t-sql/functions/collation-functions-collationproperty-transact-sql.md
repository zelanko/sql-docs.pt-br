---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f47c45f892618120b06a17f45f5d3155e092987a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funções de agrupamento – COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna a propriedade de um agrupamento especificado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*collation_name*  
É o nome do agrupamento. *collation_name* é **nvarchar(128)** e não tem padrão.
  
*property*  
É a propriedade do agrupamento. *property* é **varchar(128)** e pode ser um dos seguintes valores:
  
|Nome da propriedade|Description|  
|---|---|
|**CodePage**|Página de código de não Unicode do agrupamento. Consulte [Apêndice G: Tabelas de mapeamento do DBCS/Unicode](https://msdn.microsoft.com/en-us/library/cc194886.aspx) e [Apêndice H: Páginas de código](https://msdn.microsoft.com/en-us/library/cc195051.aspx) para converter esses valores e ver seus mapeamentos de caracteres.|  
|**LCID**|Windows LCID do agrupamento. Consulte [Estrutura de LCID](https://msdn.microsoft.com/en-us/library/cc233968.aspx) para converter esses valores (você precisará converter **varbinary** primeiro).|  
|**ComparisonStyle**|Estilo de comparação do agrupamento do Windows. Retorna 0 para todos os agrupamentos binários, (\_BIN) e (\_BIN2), bem como quando todas as propriedades são confidenciais. Valores de bitmask:<br /><br /> Ignorar maiúsculas e minúsculas: 1<br /><br /> Ignorar acento: 2<br /><br /> Ignorar Kana: 65536<br /><br /> Ignorar largura: 131072<br /><br /> Observação: embora isso afete o comportamento da comparação, a opção diferenciação de seletor de variação (\_VSS) não é representada nesse valor.|  
|**Versão**|A versão do agrupamento, extraída do campo de versão da identificação do agrupamento. Retorna um valor inteiro entre 0 e 3.<br /><br /> Agrupamentos com "140" no nome retornam 3.<br /><br /> Agrupamentos com "100" no nome retornam 2.<br /><br /> Agrupamentos com "90" no nome retornam 1.<br /><br /> Todos os outros agrupamentos retornam 0.|  
  
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
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Consulte também
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

