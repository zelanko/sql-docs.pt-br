---
title: "Sinônimos de tipo de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07b4ada74ee54bf1c892e0938dd794e17ea4c0cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-synonyms-transact-sql"></a>Sinônimos de tipo de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Os sinônimos de tipos de dados são incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para compatibilidade com o padrão ISO. A tabela a seguir lista os sinônimos e os tipos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os quais são mapeados.
  
|Sinônimo|Tipo de dados do sistema SQL Server|  
|---|---|
|**Binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(** *n* **)**|**char(n)**|  
|**character varying(** *n* **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Precisão dupla**|**float**|  
|**float**[**(***n***)**] para *n* = 1-7|**real**|  
|**float**[**(***n***)**] para *n* = 8-15|**float**|  
|**inteiro**|**int**|  
|**national character(** *n* **)**|**nchar(n)**|  
|**national char(** *n* **)**|**nchar(n)**|  
|**national character varying(** *n* **)**|**nvarchar(n)**|  
|**national char varying(** *n* **)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
Os sinônimos de tipo de dados podem ser usados no lugar do nome do tipo de dados base correspondente em instruções DDL (linguagem de definição de dados), como CREATE TABLE, CREATE PROCEDURE ou DECLARE *@variable*. Entretanto, depois que o objeto é criado, os sinônimos não têm nenhuma visibilidade. Quando o objeto é criado, é atribuído a ele o tipo de dados base associado ao sinônimo. Não há nenhum registro de que o sinônimo foi especificado na instrução que criou o objeto.
  
O tipo de dados base é atribuído a todos os objetos derivados do objeto original, como expressões ou colunas de conjuntos de resultados. Todas as funções de metadados subsequentes executadas no objeto original e em objetos derivados informarão o tipo de dados base, não o sinônimo. Esse comportamento ocorre com operações de metadados, como **sp_help** e outros procedimentos armazenados de sistema, as exibições de esquema de informações ou as várias operações de metadados da API de acesso a dados que informam os tipos de dados de tabela ou colunas de conjuntos de resultados.
  
Por exemplo, você pode criar uma tabela especificando `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` é, na realidade, atribuído a um tipo de dados **nvarchar(10)**, e todas as funções de metadados subsequentes relatarão a coluna como **nvarchar(10)**. As funções de metadados nunca serão informadas como uma coluna **national character varying(10)**.
  
## <a name="see-also"></a>Consulte também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
