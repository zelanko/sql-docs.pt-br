---
title: Criar consultas com parâmetros não nomeados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cded2c0d31e4dc5527a4667f60c7403265a666cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33047183"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Criar consultas com parâmetros não nomeados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar uma consulta com um parâmetro não nomeado especificando um ponto de interrogação (?) com um espaço reservado para um valor literal. O Designer de Consulta e Exibição lhe dará um nome temporário. É possível especificar vários parâmetros não nomeados na consulta, na medida do necessário.  
  
Quando você executar a consulta no Designer de Consulta e Exibição, a caixa de diálogo Parâmetros de Consulta será exibida com o nome temporário.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Para especificar um parâmetro não nomeado  
  
1.  Adicione as colunas ou expressões que você deseja pesquisar no painel [Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md). Se você não quiser que as colunas ou expressões a ser pesquisadas apareçam na saída da consulta, remova-as como colunas de saída.  
  
2.  Localize a linha contendo a expressão ou coluna de dados a ser pesquisada e, depois, na coluna de grade **Filtro** digite um ponto de interrogação (?).  
  
    Por padrão, o Designer de Consulta e Exibição adiciona o operador "=". Porém, você poderá editar a célula para substituir ">", "<", ou qualquer outro operador de comparação de SQL.  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
