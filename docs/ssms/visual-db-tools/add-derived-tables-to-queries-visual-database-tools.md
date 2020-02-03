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
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: b36b4774386343ee691cfa455787cf093639ce07
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253437"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>Adicionar tabelas derivadas a consultas (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
