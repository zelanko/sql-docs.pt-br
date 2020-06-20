---
title: Definindo colunas e tabelas UDT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: aa9596629ed8b4877b1793fa0c56956c52989499
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954526"
---
# <a name="defining-udt-tables-and-columns"></a>Definindo tabelas e colunas UDT
  Depois que o assembly que contém a definição de UDT (tipo definido pelo usuário) tiver sido registrado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, ele poderá ser usado em uma definição de coluna.  
  
## <a name="creating-tables-with-udts"></a>Criando tabelas com UDTs  
 Não há nenhuma sintaxe especial para criar uma coluna UDT em uma tabela. Você pode usar o nome do UDT em uma definição de coluna como se ele fosse um dos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intrínsecos. A instrução CREATE TABLE a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] cria uma tabela chamada **Points**, com uma coluna chamada **ID,** que é definida como uma `int` coluna de identidade e a chave primária da tabela. A segunda coluna é nome **PointValue**, com um tipo de dados de **Point**. O nome do esquema usado neste exemplo é **dbo**. Observe que você precisa ter as permissões necessárias para especificar um nome de esquema. Se você omitir o nome do esquema, será usado o esquema padrão do usuário de banco de dados.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Criando índices em colunas UDT  
 Há duas opções para indexar uma coluna UDT:  
  
-   Indexar o valor cheio. Neste caso, se o UDT tiver ordem binária, você poderá criar um índice de toda a coluna UDT usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX.  
  
-   Indexar expressões UDT. Você pode criar índices em colunas computadas persistidas das expressões UDT. A expressão UDT pode ser um campo, um método ou uma propriedade de um UDT. A expressão deve ser determinística e não deve acessar dados.  
  
 Para obter mais informações, consulte [tipos CLR definidos pelo usuário](clr-user-defined-types.md) e [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com tipos de dados definidos pelo usuário no SQL Server](working-with-user-defined-types-in-sql-server.md)  
  
  
