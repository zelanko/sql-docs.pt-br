---
title: Definindo tabelas e colunas UDT | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7fb463a9cf7cde943357ae7b1f3da8ed1dbfb253
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>Trabalhando com tipos definidos pelo usuário - definição de colunas e tabelas UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Depois que o assembly que contém o tipo definido pelo usuário (UDT) definição foi registrada em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, ele pode ser usado em uma definição de coluna.  
  
## <a name="creating-tables-with-udts"></a>Criando tabelas com UDTs  
 Não há nenhuma sintaxe especial para criar uma coluna UDT em uma tabela. Você pode usar o nome do UDT em uma definição de coluna como se ele fosse um dos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intrínsecos. A tabela a seguir criar [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução cria uma tabela denominada **pontos**, com uma coluna chamada **ID,** que é definida como um **int** coluna de identidade e o chave primária da tabela. A segunda coluna é denominada **PointValue**, com um tipo de dados de **ponto**. O nome de esquema usado neste exemplo é **dbo**. Observe que você precisa ter as permissões necessárias para especificar um nome de esquema. Se você omitir o nome do esquema, será usado o esquema padrão do usuário de banco de dados.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Criando índices em colunas UDT  
 Há duas opções para indexar uma coluna UDT:  
  
-   Indexar o valor cheio. Neste caso, se o UDT tiver ordem binária, você poderá criar um índice de toda a coluna UDT usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX.  
  
-   Indexar expressões UDT. Você pode criar índices em colunas computadas persistidas das expressões UDT. A expressão UDT pode ser um campo, um método ou uma propriedade de um UDT. A expressão deve ser determinística e não deve acessar dados.  
  
 Para obter mais informações, consulte [tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) e [CREATE INDEX & #40; Transact-SQL & #41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com tipos definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
