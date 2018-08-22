---
title: sys. fn_helpcollations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f7a11920763d82ec7ed36a22509f2a6ef0ce80b2
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40395012"
---
# <a name="sysfnhelpcollations-transact-sql"></a>sys.fn_helpcollations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma lista de todos os agrupamentos com suporte.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 **fn_helpcollations** retorna as informações a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|Nome|**sysname**|Nome de agrupamento padrão|  
|Description|**nvarchar(1000)**|Descrição do agrupamento.|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a agrupamentos do Windows. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte a um número limitado (<80) de agrupamentos chamados de agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram desenvolvidos antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar suporte a agrupamentos do Windows. Os agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda têm suporte para compatibilidade com versões anteriores, mas não devem ser usados para novos trabalhos de desenvolvimento. Para obter mais informações sobre o agrupamento do Windows, veja [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md). Para obter mais informações sobre agrupamentos, consulte [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os nomes de agrupamento que começam com a letra `L` e que são agrupamentos de classificação binária.  
  
```  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```    
  
## <a name="see-also"></a>Consulte também  
[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Suporte ao agrupamento de banco de dados do Azure SQL Data Warehouse](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  

