---
title: Implementando uma junção externa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 67084043-6b23-4975-b9db-6e49923d4bab
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ffbf7857c83f9be53c8747c210736f242f04dd48
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393114"
---
# <a name="implementing-an-outer-join"></a>Implementando uma junção externa
  A junção externa não tem suporte em procedimentos armazenados compilados nativamente. O exemplo a seguir mostra uma maneira de implementar a funcionalidade de uma junção externa esquerda em um procedimento armazenado compilado nativamente.  
  
 Os exemplos usam uma variável de tabela para simular um cursor no lado esquerdo da junção e um único conjunto de resultados de uma variável de tabela, que só é adequado ao processar um número limitado de linhas, pois isso envolve a criação de uma cópia adicional das linhas de dados.  
  
 Uma variável (@outer) do tipo t1_type é usada para iterar nas linhas de t1, usando um while loop para simular um cursor. A variável @result do tipo t1t2_join_type é usada para construir o conjunto de resultados.  
  
 Você deve testar o desempenho dessa solução alternativa, para garantir que ela seja executada como esperado em seu aplicativo.  
  
```  
-- original query:  
select   
   t1.c1 as t1c1,  
   t1.c2 as t1c2,  
   t2.c2 as t2c2,  
   t2.c3 as t2c3  
   from t1 left join t2 on t1.c2=t2.c3  
GO  
  
create table dbo.t1  
(c1 int not null primary key nonclustered,  
c2 int not null) with (memory_optimized=on)  
  
create table dbo.t2  
(c2 int not null primary key nonclustered,  
c3 int not null) with (memory_optimized=on)  
  
INSERT t1 VALUES (1,2)  
INSERT t1 VALUES (2,3)  
INSERT t1 VALUES (3,2)  
INSERT t2 VALUES (2,3)  
INSERT t2 VALUES (4,3)  
GO  
  
create type dbo.t1_type as table  
(  
   id int identity not null primary key nonclustered hash with (bucket_count=1024),  
   c1 int,  
   c2 int  
) with (memory_optimized=on)  
GO  
  
create type dbo.t1t2_join_type as table  
(  
   t1c1 int not null index ix_t1c1,  
   t1c2 int not null,  
   t2c2 int,  
   t2c3 int  
) with (memory_optimized=on)  
GO  
  
-- ====== scenario: generic left join  
  
-- stored procedure including the workaround  
create procedure dbo.usp_left_join  
with native_compilation, execute as owner, schemabinding  
as  
begin atomic with (transaction isolation level = snapshot, language = N'us_english')  
  
   DECLARE @outer dbo.t1_type  
   DECLARE @result dbo.t1t2_join_type  
  
   -- populate the variable used for iterating over the outer rows  
   INSERT @outer(c1, c2) select c1,c2 from dbo.t1  
  
   DECLARE @i int = 1  
   DECLARE @max int = scope_identity()  
  
   DECLARE @t1c1 int  
   DECLARE @t1c2 int  
  
   while @i <= @max  
   begin     
      select @t1c1 = c1, @t1c2 = c2 from @outer where id = @i  
  
      INSERT @result select @t1c1, @t1c2, c2, c3 from dbo.t2 where c3 = @t1c2  
  
      if @@rowcount = 0   
         INSERT @result (t1c1, t1c2) VALUES (@t1c1, @t1c2)  
  
      set @i += 1  
   end  
  
   select   
      t1c1,  
      t1c2,  
      t2c2,  
      t2c3  
   from @result  
end  
GO  
  
exec dbo.usp_left_join  
```  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
