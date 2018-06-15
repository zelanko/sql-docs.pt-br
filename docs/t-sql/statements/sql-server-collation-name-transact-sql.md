---
title: Nome de agrupamento do SQL Server (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 136cb86368a360b6f50be5af8e94a38292fb1a1f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33071583"
---
# <a name="sql-server-collation-name-transact-sql"></a>Nome de agrupamento do SQL Server (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É uma única cadeia de caracteres que especifica o nome de agrupamento para um agrupamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a agrupamentos do Windows. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte a um número limitado (<80) de agrupamentos chamados de agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram desenvolvidos antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar suporte a agrupamentos do Windows. Os agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda têm suporte para compatibilidade com versões anteriores, mas não devem ser usados para novos trabalhos de desenvolvimento. Para obter mais informações sobre o agrupamento do Windows, veja [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>Argumentos  
 *SortRules*  
 Uma cadeia de caracteres identificando o alfabeto ou idioma cujas regras de classificação são aplicadas quando a classificação de dicionário é especificada. Exemplos são Latin1_General ou polonês.  
  
 **Pref**  
 Especifica a preferência por maiúsculas. Mesmo se a comparação diferenciar maiúsculas de minúsculas, a versão em maiúsculas de uma letra vem antes da versão em minúsculas, quando não há outra distinção.  
  
 *Codepage*  
 Especifica um número de um a quatro dígitos que identifica a página de código usada pelo agrupamento. **CP1** especifica a página de código 1252 para todas as outras páginas de código para as quais o número de página de código completo é especificado. Por exemplo, **CP1251** especifica a página de código 1251 e **CP850** especifica a página de código 850.  
  
 *CaseSensitivity*  
 **CI** especifica que não diferencia maiúsculas de minúsculas, **CS** especifica que diferencia maiúsculas de minúsculas.  
  
 *AccentSensitivity*  
 **AI** especifica que não diferencia acentos, **AS** especifica que diferencia acento.  
  
 **BIN**  
 Especifica a ordem de classificação binária que será usada.  
  
## <a name="remarks"></a>Remarks  
 Para listar os agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suportados pelo servidor, execute a seguinte consulta.  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  Para a ID de Ordem de Classificação 80, use qualquer agrupamento do Windows com a página de código 1250 e ordem binária. Por exemplo: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Constants &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
