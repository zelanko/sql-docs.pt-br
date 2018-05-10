---
title: _ (curinga – corresponder a um caractere) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb82b8abe1b5a7d37fc74945dfc82ccce1882740
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Curinga – corresponde a um caractere) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Use o caractere sublinhado _ para corresponder a qualquer caractere único em uma operação de comparação de cadeia de caracteres que envolva correspondência de padrões, como `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Exemplos  

## <a name="a-simple-example"></a>A: Exemplo simples   

O exemplo a seguir retorna todos os nomes de banco de dados que começam com a letra `m` e têm a letra `d` como a terceira letra. O caractere sublinhado especifica que o segundo caractere do nome pode ser qualquer letra. Os bancos de dados `model` e `msdb` atendem a esse critério. O banco de dados `master` não atende.

```sql
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
Pode haver bancos de dados adicionais que atendem a esses critérios.

Você pode usar vários sublinhados para representar vários caracteres. Alterar o critério `LIKE` para incluir dois sublinhados `'m__%`, inclui o banco de dados mestre no resultado.

### <a name="b-more-complex-example"></a>B: Exemplo mais complexo
 O exemplo a seguir usa o operador _ para localizar todas as pessoas na tabela `Person` que têm um nome de três letras que termina com `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: usando escape para o caractere sublinhado   
O exemplo a seguir retorna os nomes das funções de banco de dados fixas como `db_owner` e `db_ddladmin`, mas também retorna o usuário `dbo`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

O sublinhado na posição do terceiro caractere é interpretado como um caractere curinga e não está filtrando somente entidades de segurança que começam com as letras `db_`. Para usar um escape no caractere sublinhado coloque-o entre colchetes `[_]`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Agora o usuário `dbo` foi excluído.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (Curinga – caracteres para não correspondência)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
