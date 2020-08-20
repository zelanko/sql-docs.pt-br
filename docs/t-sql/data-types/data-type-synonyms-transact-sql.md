---
description: Sinônimos de tipo de dados (Transact-SQL)
title: Sinônimos de tipo de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f689cdae7253c43ca39c06dc09953c4db02d0def
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479919"
---
# <a name="data-type-synonyms-transact-sql"></a>Sinônimos de tipo de dados (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Os sinônimos de tipos de dados são incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para compatibilidade com o padrão ISO. A tabela a seguir lista os sinônimos e os tipos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os quais são mapeados.
  
|Sinônimo|Tipo de dados do sistema SQL Server|  
|---|---|
|**Binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(**_n_**)**|**char(n)**|  
|**character varying(**_n_**)**|**varchar(n)**|  
|**Dez**|**decimal**|  
|**Precisão dupla**|**float**|  
|**float**[ **(** _n_ **)** ] para _n_ = 1-7|**real**|  
|**float**[ **(** _n_ **)** ] para _n_ = 8-15|**float**|  
|**inteiro**|**int**|  
|**national character(**_n_**)**|**nchar(n)**|  
|**national char(**_n_**)**|**nchar(n)**|  
|**national character varying(**_n_**)**|**nvarchar(n)**|  
|**national char varying(**_n_**)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
Os sinônimos de tipo de dados podem ser usados no lugar do nome do tipo de dados base correspondente em instruções DDL (linguagem de definição de dados). Essas instruções incluem as *\@variáveis* CREATE TABLE, CREATE PROCEDURE e DECLARE. Entretanto, depois que o objeto é criado, os sinônimos não têm nenhuma visibilidade. Quando o objeto é criado, é atribuído a ele o tipo de dados base associado ao sinônimo. Não há nenhum registro de que o sinônimo foi especificado na instrução que criou o objeto.
  
O tipo de dados base é atribuído aos objetos derivados do objeto original, como expressões ou colunas de conjuntos de resultados. Todas as funções de metadados que usam o objeto original ou qualquer objeto derivado relatarão o tipo de dados base, não o sinônimo, incluindo:

* operações de metadados, como **sp_help** e outros procedimentos armazenados do sistema,
* exibições do esquema de informações e
* operações de metadados da API de acesso a dados que relatam os tipos de dados das colunas da tabela ou do conjunto de resultados.
  
Por exemplo, você pode criar uma tabela especificando `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` é atribuído a um tipo de dados **nvarchar(10)**, e todas as funções de metadados seguintes relatarão a coluna como **nvarchar(10)**. As funções de metadados nunca serão informadas como uma coluna **national character varying(10)**.
  
## <a name="see-also"></a>Confira também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
