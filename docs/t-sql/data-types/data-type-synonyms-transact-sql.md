---
title: "Tipo de dados sinônimos (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d9b1da2bdc7084268740cd7de2580e64ee9698b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-synonyms-transact-sql"></a>Sinônimos de tipos de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Os sinônimos de tipos de dados são incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para compatibilidade com o padrão ISO. A tabela a seguir lista os sinônimos e os tipos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os quais são mapeados.
  
|Sinônimo|Tipo de dados do sistema SQL Server|  
|---|---|
|**A variável binário**|**varbinary**|  
|**char variados**|**varchar**|  
|**caractere**|**char**|  
|**caractere**|**char (1)**|  
|**caractere (**  *n*  **)**|**char(n)**|  
|**variável de caractere (**  *n*  **)**|**varchar(n)**|  
|**DEC**|**decimal**|  
|**Precisão dupla**|**float**|  
|**float**[**(***n***)**] para  *n*  = 1-7|**real**|  
|**float**[**(***n***)**] para  *n*  = 8-15|**float**|  
|**inteiro**|**int**|  
|**caractere Nacional (**  *n*  **)**|**nchar (n)**|  
|**National char (**  *n*  **)**|**nchar (n)**|  
|**variável de caractere Nacional (**  *n*  **)**|**nvarchar (n)**|  
|**variável de caractere Nacional (**  *n*  **)**|**nvarchar (n)**|  
|**texto nacional**|**ntext**|  
|**timestamp**|rowversion|  
  
Sinônimos de tipo de dados pode ser usados em vez do nome de tipo de dados base correspondente em instruções de DDL (linguagem) de definição de dados, como CREATE TABLE, CREATE PROCEDURE ou DECLARE  *@variable* . Entretanto, depois que o objeto é criado, os sinônimos não têm nenhuma visibilidade. Quando o objeto é criado, é atribuído a ele o tipo de dados base associado ao sinônimo. Não há nenhum registro de que o sinônimo foi especificado na instrução que criou o objeto.
  
O tipo de dados base é atribuído a todos os objetos derivados do objeto original, como expressões ou colunas de conjuntos de resultados. Todas as funções de metadados subsequentes executadas no objeto original e em objetos derivados informarão o tipo de dados base, não o sinônimo. Esse comportamento ocorre com operações de metadados, como **sp_help** e outros sistemas de procedimentos armazenados, exibições do esquema de informações ou as várias operações de metadados de API de acesso de dados que tipos de dados da tabela ou conjunto de resultados de relatório colunas.
  
Por exemplo, você pode criar uma tabela especificando `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`é atribuído um **nvarchar (10)** tipo de dados, e todas as funções de metadados subsequentes informarão a coluna como um **nvarchar (10)** coluna. As funções de metadados nunca serão informadas como uma **varying(10) de caractere nacional** coluna.
  
## <a name="see-also"></a>Consulte também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

