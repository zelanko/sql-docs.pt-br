---
title: Nome de ordenação do SQL Server (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f08564eb8821df4d25bf352ae3afce8afbc7dae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62928666"
---
# <a name="sql-server-collation-name-transact-sql"></a>Nome de ordenação do SQL Server (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

É uma única cadeia de caracteres que especifica o nome de ordenação para uma ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a ordenações do Windows. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também dá suporte a um número limitado (&lt;80) de ordenações chamadas ordenações de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que foram desenvolvidas antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar suporte a ordenações do Windows. As ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda têm suporte para compatibilidade com versões anteriores, mas não devem ser usados para novos trabalhos de desenvolvimento. Para obter mais informações sobre a ordenação do Windows, consulte [Nome de ordenação do Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```
<SQL_collation_name> :: =
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>

<ComparisonStyle> ::=
_CaseSensitivity_AccentSensitivity | _BIN
```

## <a name="arguments"></a>Argumentos

*SortRules* Uma cadeia de caracteres identificando o alfabeto ou idioma cujas regras de classificação são aplicadas quando a classificação de dicionário é especificada. Exemplos são Latin1_General ou polonês.

**Pref** Especifica a preferência por maiúsculas. Mesmo se a comparação diferenciar maiúsculas de minúsculas, a versão em maiúsculas de uma letra vem antes da versão em minúsculas, quando não há outra distinção.

*Codepage* Especifica um número de um a quatro dígitos que identifica a página de código usada pela ordenação. **CP1** especifica a página de código 1252 para todas as outras páginas de código para as quais o número de página de código completo é especificado. Por exemplo, **CP1251** especifica a página de código 1251 e **CP850** especifica a página de código 850.

*CaseSensitivity*
**CI** especifica que não diferencia maiúsculas de minúsculas, **CS** especifica que diferencia maiúsculas de minúsculas.

*AccentSensitivity*
**AI** especifica que não diferencia acentos, **AS** especifica que diferencia acento.

**BIN** Especifica a ordem de classificação binária que será usada.

## <a name="remarks"></a>Remarks

Para listar as ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suportados pelo servidor, execute a seguinte consulta.

```sql
SELECT * FROM sys.fn_helpcollations()
WHERE name LIKE 'SQL%';
```

> [!NOTE]
> Para a ID de Ordem de Classificação 80, use qualquer ordenação do Windows com a página de código 1250 e ordem binária. Por exemplo: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.

## <a name="see-also"></a>Consulte Também

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [Constantes](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [table](../../t-sql/data-types/table-transact-sql.md)
- [sys.fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
