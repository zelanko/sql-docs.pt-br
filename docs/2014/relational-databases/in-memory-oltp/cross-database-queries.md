---
title: Consultas de bancos de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b86fb120d8263ae48bb9a4e874e4cf0d012bf7a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050213"
---
# <a name="cross-database-queries"></a>Consultas de bancos de dados
  No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], as tabelas com otimização de memória não oferecem suporte a transações envolvendo todos os bancos de dados. Você não pode acessar outro banco de dados da mesma transação ou na mesma consulta que também acesse uma tabela com otimização de memória. Você não pode copiar facilmente dados de uma tabela em um banco de dados, para uma tabela com otimização de memória em outro banco de dados.  
  
 Variáveis de tabela não são transacionais. Assim, as variáveis de tabela com otimização de memória podem ser usadas em consultas de bancos de dados e, portanto, podem facilitar a movimentação de dados de um banco de dados para tabelas com otimização de memória em outro. Você pode usar duas transações. Na primeira transação, insira os dados da tabela remota na variável. Na segunda transação, insira os dados na tabela com otimização de memória local da variável.  
  
 Por exemplo, para copiar a linha da tabela T1 no banco de dados db1 para a tabela T2 no DB2, usando a variável @v1 do tipo dbo. TT1, você pode usar algo como:  
  
```sql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
