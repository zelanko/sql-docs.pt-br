---
title: "Criar consultas com parâmetros não nomeados (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: abd2c8d121a7f3e536c30324c1f4f83ae323795e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Criar consultas com parâmetros não nomeados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode criar uma consulta com um parâmetro não nomeado especificando um ponto de interrogação (?) com um espaço reservado para um valor literal. O Designer de Consulta e Exibição lhe dará um nome temporário. É possível especificar vários parâmetros não nomeados na consulta, na medida do necessário.  
  
Quando você executar a consulta no Designer de Consulta e Exibição, a caixa de diálogo Parâmetros de Consulta será exibida com o nome temporário.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Para especificar um parâmetro não nomeado  
  
1.  Adicione as colunas ou expressões que você deseja pesquisar no painel [Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md). Se você não quiser que as colunas ou expressões a ser pesquisadas apareçam na saída da consulta, remova-as como colunas de saída.  
  
2.  Localize a linha contendo a expressão ou coluna de dados a ser pesquisada e, depois, na coluna de grade **Filtro** digite um ponto de interrogação (?).  
  
    Por padrão, o Designer de Consulta e Exibição adiciona o operador "=". Porém, você poderá editar a célula para substituir ">", "<", ou qualquer outro operador de comparação de SQL.  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
