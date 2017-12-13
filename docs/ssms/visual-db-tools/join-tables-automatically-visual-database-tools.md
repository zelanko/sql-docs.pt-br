---
title: Unir tabelas automaticamente (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8cc25439ca691c45e81f51bb5554a87162f052c2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="join-tables-automatically-visual-database-tools"></a>Unir tabelas automaticamente (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Quando você adiciona duas ou mais tabelas a uma consulta, o [Designer de Exibição e Consulta](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) tenta determinar se elas estão relacionadas. Se estiverem, o Designer de Consulta e Exibição unirá automaticamente linhas de junção entre os retângulos que representam as tabelas ou objetos estruturados por tabela.  
  
O Designer de Consulta e Exibição reconhecerá tabelas como unidas se:  
  
-   O banco de dados contiver informações que especifica que as tabelas estão relacionadas.  
  
-   Se duas colunas, uma em cada tabela, tiverem o mesmo nome e tipo de dados. A coluna deve ser uma chave primária em pelo menos uma das tabelas. Por exemplo, se você adicionar as tabelas `employee` e `jobs` , se a coluna `job_id` for a chave primária na tabela `jobs` , e se cada tabela tiver uma coluna chamada `job_id` com o mesmo tipo de dados, o Designer de Consulta e Exibição unirá as tabelas automaticamente.  
  
    > [!NOTE]  
    > O Designer de Consulta e Exibição criará somente uma junção com base nas colunas com o mesmo nome e tipo de dados. Se for possível mais de uma união, o Designer de Consulta e Exibição será interrompido depois de criar uma união com base no primeiro conjunto de colunas coincidentes que encontrar.  
  
-   O Designer de Consulta e Exibição detecta que um critério de pesquisa (uma cláusula WHERE) é, de fato, uma condição de junção. Por exemplo, você pode adicionar as tabelas `employee` e `jobs`e, depois criar um critério de pesquisa que procure o mesmo valor na coluna `job_id` das duas tabelas. Quando você fizer isso, o Designer de Consulta e Exibição detecta que o critério de pesquisa resulta em uma junção e, depois, cria uma condição de junção baseado no critério de pesquisa.  
  
Se o Designer de Consulta e Exibição criou uma junção não adequada à sua consulta, você poderá modificar a junção ou removê-la. Para obter detalhes, consulte [Modificar operadores de junção &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md) e [Remover junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md).  
  
Se o Designer de Consulta e Exibição não unir automaticamente as tabelas em sua consulta, você poderá criar uma junção. Para obter detalhes, consulte [Unir tabelas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte também  
[Como o Designer de Consulta e Exibição representa junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
