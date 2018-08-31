---
title: 'Lição 3: Marcar como tabela de data | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cb63b6cb67303dd763263b7d9dbeea30cfc4e3b
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42791977"
---
# <a name="lesson-3-mark-as-date-table"></a>Lição 3: marcar como tabela de data
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Na lição 2: Adicionar Dados, você importou uma tabela de dimensão chamada DimDate. Enquanto no seu modelo essa tabela é denominada DimDate, ela também é conhecida como uma *tabela de data*, que contém dados de data e hora.  
  
Sempre que você pode usar funções de inteligência de tempo DAX em cálculos, como você fará quando você cria medidas um pouco mais tarde, você deve especificar as propriedades de tabela de data, que incluem uma *tabela de datas* e um identificador exclusivo *data coluna* nessa tabela.
  
Nesta lição, você irá marcar a tabela DimDate, como o *tabela de datas* e a coluna de data (na tabela de data) como o *coluna data* (identificador exclusivo).  

Antes que marcamos a tabela de data e a coluna de data, precisamos fazer uma pequena limpeza para facilitar a compreensão de nosso modelo. Você observará na tabela DimDate uma coluna denominada **FullDateAlternateKey**. Ele contém uma linha para cada dia em cada ano civil incluído na tabela. Usaremos muito essa coluna em fórmulas de medida e em relatórios. Mas, FullDateAlternateKey não é realmente um bom identificador para essa coluna. Podemos vou renomeá-lo para **data**, tornando mais fácil de identificar e incluir em fórmulas. Sempre que possível, é uma boa ideia para renomear objetos, como tabelas e colunas para torná-los mais fáceis de identificar no cliente de relatório de aplicativos, como o Power BI e Excel. 
  
Tempo estimado para concluir esta lição: **3 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 2: adicionar dados](../analysis-services/lesson-2-add-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para renomear a coluna FullDateAlternateKey

1.  No designer de modelo, clique o **DimDate** tabela.

2.  Clique duas vezes o cabeçalho para o **FullDateAlternateKey** coluna e, em seguida, renomeie-o como **data**.

  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  Selecione a coluna **Data** e, na janela **Propriedades** , em **Tipo de Dados**, verifique se a opção  **Data** está selecionada.  
  
2.  Clique no menu **Tabela** , clique em **Data**e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo. Geralmente, ele será selecionado por padrão. Clique em **OK**. 

    ![como tabular-lição 3-data-tabela](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 4: criar relações](../analysis-services/lesson-4-create-relationships.md).
  
