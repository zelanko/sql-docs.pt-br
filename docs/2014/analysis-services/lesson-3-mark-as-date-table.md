---
title: 'Lição 4: Marcar como tabela de data | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a2a6ce44a66fbb1e9045116580acc726f648df9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265742"
---
# <a name="lesson-4-mark-as-date-table"></a>Lição 4: Marcar como Tabela de Data
  Na lição 2: Adicionar Dados, você importou uma tabela de dimensão chamada DimDate. Você renomeou a tabela DimDate, na Lição 3: Renomear Colunas, como simplesmente Data. Em seu modelo, essa tabela agora é chamada Date; ela também pode ser conhecida como uma *tabela Data*, pois contém dados de data e hora.  
  
 Sempre que você usar funções de Inteligência de Dados Temporais em cálculos, como fará quando criar medidas mais adiante, especifique as propriedades da tabela de data, que inclui uma *tabela de Data* e uma *coluna de Data* de identificador exclusivo nessa tabela. Você pode criar relações válidas entre outras tabelas e a tabela de Data; necessário para cálculos que usam funções de inteligência de tempo DAX.  
  
 Nesta lição, você aprenderá a marcar a tabela de Data importada e renomeada como a *tabela de Data* e a coluna de Data (na tabela de Data) como a *coluna de Data* (identificador exclusivo). O uso do nome Data pode ficar confuso, mas isso logo se esclarecerá.  
  
 Tempo estimado para concluir esta lição: **3 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 3: Renomear colunas](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  No designer de modelos, clique na tabela **Data** (guia).  
  
2.  Clique no menu **Tabela**, clique em **Data** e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 5: Criar relações](lesson-4-create-relationships.md).  
  
  
