---
title: Adicionar Tabelas Derivadas a Consultas
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [Visual Database Tools]
- joins [SQL Server], derived tables
- table joins [SQL Server]
- derived tables
ms.assetid: 05f1ba1d-465f-4e36-84bb-21b963c9b8f9
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: a234da70206c87387b38f55b64304f6ed8e31dc9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009330"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>Adicionar tabelas derivadas a consultas (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
As tabelas derivadas são conjuntos de resultados usados como origens de tabela em uma consulta. Você pode adicionar uma tabela derivada a uma consulta no painel **Diagrama**.  
  
### <a name="to-add-a-derived-table-to-a-query"></a>Para adicionar uma tabela derivada a uma consulta  
  
1.  Abra uma consulta existente ou crie uma nova consulta.  
  
2.  Clique com o botão direito do mouse no painel **Diagrama** e selecione **Adicionar Nova Tabela Derivada**.  
  
    Uma nova tabela com o nome derivedtbl_*N* é adicionada, e a instrução SELECT da tabela derivada é adicionada à cláusula FROM da consulta.  
  
## <a name="see-also"></a>Consulte Também  
[Executar operações básicas com consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Criar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Abrir consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)  
[SELECT (Transact-SQL)](https://msdn.microsoft.com/dc85caea-54d1-49af-b166-f3aa2f3a93d0)  
  
