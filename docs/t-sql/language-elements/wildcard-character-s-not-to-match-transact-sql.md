---
title: '[^] Curinga para excluir caracteres'
description: O curinga T-SQL para caracteres não corresponde
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
author: rothja
ms.author: jroth
ms.openlocfilehash: e7291bc39092d4f65fd69f8c4050bb52a512ef04
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76831733"
---
# <a name="-wildcard---characters-not-to-match-transact-sql"></a>\[^\] (Curinga – caracteres para não correspondência) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Corresponde a qualquer caractere único que esteja fora do intervalo ou conjunto especificado entre colchetes `[^]`. Esses caracteres curinga podem ser usados em comparações de cadeias de caracteres que envolvem a correspondência de padrões, como `LIKE` e `PATINDEX`. 
  
## <a name="examples"></a>Exemplos  
### <a name="a-simple-example"></a>A: Exemplo simples   
 O exemplo a seguir usa o operador [^] para localizar as cinco primeiras pessoas na tabela `Contact` cujo nome começa com `Al` e tem uma terceira letra diferente de `a`.  
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP 5 FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%';  
```  
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
FirstName     LastName
---------     --------
Alex          Adams
Alexandra     Adams
Allison       Adams
Alisha        Alan
Alexandra     Alexander
```
### <a name="b-searching-for-ranges-of-characters"></a>B: Pesquisando intervalos de caracteres

Um conjunto de curingas pode incluir caracteres únicos ou intervalos de caracteres, bem como combinações de caracteres e intervalos. O exemplo a seguir usa o operador [^] para localizar uma cadeia de caracteres que não começa com uma letra ou número.

```sql
SELECT [object_id], OBJECT_NAME(object_id) AS [object_name], name, column_id 
FROM sys.columns 
WHERE name LIKE '[^0-9A-z]%';
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
object_id     object_name   name    column_id
---------     -----------   ----    ---------
1591676718    JunkTable     _xyz    1
```
  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [% &#40;Curinga – caracteres para correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; &#40;Curinga – caracteres para correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [\_ &#40;Curinga – encontrar a correspondência de um caractere&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  
