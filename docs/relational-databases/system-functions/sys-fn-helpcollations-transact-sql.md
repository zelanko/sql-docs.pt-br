---
title: sys. fn_helpcollations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83c9efd36bbcec788ef18b19552446877c5e36c8
ms.sourcegitcommit: 7e828cd92749899f4e1e45ef858ceb9a88ba4b6a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51629609"
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
|Nome|**sysname**|Nome de ordenação padrão|  
|Description|**nvarchar(1000)**|Descrição da ordenação.|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a ordenações do Windows. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte a um número limitado (&lt;80) de ordenações chamados de ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram desenvolvidos antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar suporte a ordenações do Windows. As ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda têm suporte para compatibilidade com versões anteriores, mas não devem ser usados para novos trabalhos de desenvolvimento. Para obter mais informações sobre a ordenação do Windows, veja [Nome de ordenação do Windows &amp;#40;Transact-SQL&amp;#41;](../../t-sql/statements/windows-collation-name-transact-sql.md). Para obter mais informações sobre ordenações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os nomes de ordenação que começam com a letra `L` e que são ordenações de classificação binária.  
  
```sql  
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

