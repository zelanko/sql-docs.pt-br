---
title: "_ (Curinga – corresponde a um caractere) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e47fdb9e12a632323971558d2e894fb7b181498e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Curinga – corresponde a um caractere) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Use o caractere de sublinhado `_` para corresponder a qualquer caractere único em uma operação de comparação de cadeia de caracteres que envolva correspondência de padrões, como `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Exemplos  

## <a name="a-simple-example"></a>R: exemplo simples de   

O exemplo a seguir retorna todos os nomes que começam com a letra de banco de dados `m` e ter a letra `d` como a terceira letra. O caractere de sublinhado Especifica que o segundo caractere do nome pode ser qualquer letra. O `model` e `msdb` bancos de dados atendem esse critério. O `master` não banco de dados.

```tsql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
Você pode ter bancos de dados adicionais que atendem aos critérios.

Você pode usar vários sublinhados para representar vários caracteres. Alterando o `LIKE` critérios para incluir dois sublinhados `'m__%` inclui o banco de dados mestre no resultado.

### <a name="b-more-complex-example"></a>B: exemplo mais complexo
 O exemplo a seguir usa o operador `_` para localizar todas as pessoas na tabela `Person` que tenham um nome com três letras e que termine com `an`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: escapar o caractere de sublinhado   
O exemplo a seguir retorna os nomes das funções fixas de banco de dados como `db_owner` e `db_ddladmin`, mas ele também retorna o `dbo` usuário. 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

O sublinhado na terceira posição de caractere será interpretado como um caractere curinga e não está filtrando para somente entidades começando com as letras `db_`. Para escapar o caractere de sublinhado coloque-o entre colchetes `[_]`. 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Agora o `dbo` usuário foi excluído.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Consulte também  
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (Curinga - caracteres não correspondência)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
  

