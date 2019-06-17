---
title: 'Lição 4: Marcar como tabela de data | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26877c4892b050cbf9c8dcc6553530dff513f8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078792"
---
# <a name="lesson-4-mark-as-date-table"></a>Lição 4: Marcar como Tabela de Data
  Lição 2: Adicionar dados, você importou uma tabela de dimensão chamada DimDate. Você renomeou a tabela DimDate, na lição 3: Renomear colunas, como simplesmente Data. Em seu modelo, essa tabela agora é chamada Date; ela também pode ser conhecida como uma *tabela Data*, pois contém dados de data e hora.  
  
 Sempre que você usar funções de Inteligência de Dados Temporais em cálculos, como fará quando criar medidas mais adiante, especifique as propriedades da tabela de data, que inclui uma *tabela de Data* e uma *coluna de Data* de identificador exclusivo nessa tabela. Você pode criar relações válidas entre outras tabelas e a tabela de Data; necessário para cálculos que usam funções de inteligência de tempo DAX.  
  
 Nesta lição, você aprenderá a marcar a tabela de Data importada e renomeada como a *tabela de Data* e a coluna de Data (na tabela de Data) como a *coluna de Data* (identificador exclusivo). O uso do nome que data pode ficar confusa, mas você receberá em breve a ideia.  
  
 Tempo estimado para concluir esta lição: **3 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 3: Renomear colunas](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  No designer de modelos, clique na tabela **Data** (guia).  
  
2.  Clique no menu **Tabela**, clique em **Data** e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 5: Criar relações](lesson-4-create-relationships.md).  
  
  
