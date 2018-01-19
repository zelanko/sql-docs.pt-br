---
title: "_ (Curinga – corresponde a um caractere) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
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
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96a529dd77d0d76ecf8fe85dba2d211c71b4c398
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Curinga – corresponde a um caractere) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Use o caractere de sublinhado _ para corresponder qualquer caractere único em uma operação de comparação de cadeia de caracteres que envolva correspondência de padrões, como `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Exemplos  

## <a name="a-simple-example"></a>R: exemplo simples de   

O exemplo a seguir retorna todos os nomes que começam com a letra de banco de dados `m` e ter a letra `d` como a terceira letra. O caractere de sublinhado Especifica que o segundo caractere do nome pode ser qualquer letra. O `model` e `msdb` bancos de dados atendem esse critério. O `master` não banco de dados.

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
Você pode ter bancos de dados adicionais que atendem aos critérios.

Você pode usar vários sublinhados para representar vários caracteres. Alterando o `LIKE` critérios para incluir dois sublinhados `'m__%` inclui o banco de dados mestre no resultado.

### <a name="b-more-complex-example"></a>B: exemplo mais complexo
 O exemplo a seguir usa o operador de _ para localizar todas as pessoas a `Person` tabela, que têm um nome três letras que termina em `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: escapar o caractere de sublinhado   
O exemplo a seguir retorna os nomes das funções fixas de banco de dados como `db_owner` e `db_ddladmin`, mas ele também retorna o `dbo` usuário. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

O sublinhado na terceira posição de caractere será interpretado como um caractere curinga e não está filtrando para somente entidades começando com as letras `db_`. Para escapar o caractere de sublinhado coloque-o entre colchetes `[_]`. 

```sql
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
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Curinga – caracteres a serem correspondidos)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (Curinga - caracteres não correspondência)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
