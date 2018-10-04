---
title: Implementando IDENTITY em uma tabela otimizada em memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c774e0b69565c21a7ba794712212e3b79bcc66e9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204036"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementando IDENTITY em uma tabela otimizada em memória
  IDENTITY(1, 1) tem suporte em uma tabela com otimização de memória. No entanto, colunas de identidade com definição de IDENTITY(x, y) onde x != 1 ou y != 1 não tem suporte em tabelas com otimização de memória. A solução alternativa para valores IDENTITY usa o objeto SEQUENCE ([Sequence Numbers](../sequence-numbers/sequence-numbers.md)).  
  
 Primeiramente, remova a propriedade IDENTITY da tabela que você está convertendo em OLTP na memória. Em seguida, defina um novo objeto SEQUENCE para a coluna na tabela. Os objetos SEQUENCE como as colunas de identidade dependem da capacidade de criar valores DEFAULT para colunas que usam a sintaxe NEXT VALUE FOR para obter um novo valor de identidade. Como não há suporte para os valores DEFAULT na OLTP na memória, você precisa passar o valor SEQUENCE recentemente gerado para a instrução INSERT ou para um procedimento armazenado nativamente compilado que faça a inserção. O exemplo a seguir demonstra esse padrão.  
  
```tsql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 Após executar a inserção várias vezes, você verá valores válidos que aumentam de forma monotônica na coluna [c1]. Esse conjunto de resultados é gerado usando a verificação de tabela e o índice de hash sem `ORDER BY` para que as linhas não sejam ordenadas.  
  
## <a name="see-also"></a>Consulte também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
