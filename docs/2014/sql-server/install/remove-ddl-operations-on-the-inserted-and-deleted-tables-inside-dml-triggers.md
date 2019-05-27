---
title: Remover operações DDL nas tabelas inseridas e excluídas em gatilhos DML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- data definition language [SQL Server]
- DDL statements [SQL Server]
- DML triggers, removing DDL operations
ms.assetid: e49ba7d5-787f-4052-b985-b699195d982b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2f0990fbe65adc97b9e654f6393e25582363596
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093125"
---
# <a name="remove-ddl-operations-on-the-inserted-and-deleted-tables-inside-dml-triggers"></a>Remover operações DDL de tabelas inseridas e excluídas em gatilhos DML
  Instruções de DDL (linguagem) de definição de dados, como CREATE INDEX, não podem ser executadas nas tabelas inseridas e excluídas em gatilhos DML. Algumas instruções DDL em tabelas inseridas e excluídas eram permitidas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte ‘Usando as tabelas inseridas e excluídas’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova quaisquer operações DDL que são executadas nas tabelas inseridas e excluídas em gatilhos DML.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
