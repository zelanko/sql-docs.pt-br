---
title: Definindo tabelas e colunas UDT | Microsoft Docs
description: Depois de registrar o conjunto que contém uma definição UDT, você pode usá-lo em uma definição de coluna.
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f46ebc5089a4cb2fdb974df52d9bc876f925da4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486885"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>Trabalhar com tipos definidos pelo usuário – Definir colunas e tabelas UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Uma vez que o conjunto contendo a definição de tipo definido [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo usuário (UDT) tenha sido registrado em um banco de dados, ele pode ser usado em uma definição de coluna. Para obter mais informações, veja [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md).  
  
## <a name="creating-tables-with-udts"></a>Criando tabelas com UDTs  
 Não há nenhuma sintaxe especial para criar uma coluna UDT em uma tabela. Você pode usar o nome do UDT em uma definição de coluna como se ele fosse um dos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intrínsecos. A seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] declaração CREATE TABLE cria uma tabela chamada **Points**, com uma coluna chamada **ID,** que é definida como uma coluna de identidade **int** e a chave principal para a tabela. A segunda coluna é chamada **PointValue**, com um tipo de dados de **Point**. O nome do esquema usado neste exemplo é **dbo**. Observe que você precisa ter as permissões necessárias para especificar um nome de esquema. Se você omitir o nome do esquema, será usado o esquema padrão do usuário de banco de dados.  
  
```sql  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Criando índices em colunas UDT  
 Há duas opções para indexar uma coluna UDT:  
  
-   **Indexar o valor cheio.** Neste caso, se o UDT tiver ordem binária, você poderá criar um índice de toda a coluna UDT usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX.  
  
-   **Indexar expressões UDT.** Você pode criar índices em colunas computadas persistidas das expressões UDT. A expressão UDT pode ser um campo, um método ou uma propriedade de um UDT. A expressão deve ser determinística e não deve acessar dados.  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com tipos definidos pelo usuário no sql server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)     
 [TIPO DE CRIAÇÃO (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)     
 [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)     
