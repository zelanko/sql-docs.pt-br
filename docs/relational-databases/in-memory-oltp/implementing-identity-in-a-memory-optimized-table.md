---
title: Implementando IDENTITY em uma tabela otimizada em memória | Microsoft Docs
description: Saiba mais sobre IDENTITY em tabelas com otimização de memória no SQL Server. As tabelas com otimização de memória dão suporte à IDENTITY para um valor de semente e de incremento de um.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 591f3fbf92d7d56c531c05e82d4eea0c5ff49abf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723181"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementando IDENTITY em uma tabela otimizada em memória
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Há suporte para IDENTITY em uma tabela com otimização de memória, desde que a semente e o incremento sejam 1 (padrão). Não há suporte em tabelas com otimização de memória para colunas de identidade com definição de IDENTITY(x, y), em que x != 1 ou y != 1.   
    
Para aumentar a semente de IDENTITY, insira uma nova linha com um valor explícito para a coluna de identidade, usando a opção de sessão `SET IDENTITY_INSERT table_name ON`. Com a inserção da linha, a semente de IDENTITY é alterada para o valor inserido explicitamente, mais 1. Por exemplo, para aumentar a semente para 1.000, insira uma linha com valor 999 na coluna de identidade. Os valores de identidade gerados serão iniciados em 1.000.     
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
