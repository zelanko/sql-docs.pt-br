---
title: Criar consultas com parâmetros não nomeados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a2245bf5298d6b760b0b52a8dc83f233d337283f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019767"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Criar consultas com parâmetros não nomeados (Visual Database Tools)
  Você pode criar uma consulta com um parâmetro não nomeado especificando um ponto de interrogação (?) com um espaço reservado para um valor literal. O Designer de Consulta e Exibição lhe dará um nome temporário. É possível especificar vários parâmetros não nomeados na consulta, na medida do necessário.  
  
 Quando você executar a consulta no Designer de Consulta e Exibição, a caixa de diálogo Parâmetros de Consulta será exibida com o nome temporário.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Para especificar um parâmetro não nomeado  
  
1.  Adicione as colunas ou expressões que você deseja pesquisar no painel [Critérios](visual-database-tools.md). Se você não quiser que as colunas ou expressões a ser pesquisadas apareçam na saída da consulta, remova-as como colunas de saída.  
  
2.  Localize a linha contendo a expressão ou coluna de dados a ser pesquisada e, depois, na coluna de grade **Filtro** digite um ponto de interrogação (?).  
  
     Por padrão, o Designer de Consulta e Exibição adiciona o operador "=". Porém, você poderá editar a célula para substituir ">", "<", ou qualquer outro operador de comparação de SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Consultar com parâmetros &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  