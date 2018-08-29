---
title: 'Lição 3 do tutorial de serviços de análise: marcar como tabela de data | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 282103baa0283e46e31b9ffe6b837e90e4bfac3c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069393"
---
# <a name="mark-as-date-table"></a>Marcar como Tabela de Data

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Na lição 2: Obter dados, você importou uma tabela de dimensão chamada **DimDate**. Enquanto no seu modelo essa tabela é denominada DimDate, ela também é conhecida como uma *tabela de data*, que contém dados de data e hora.  
  
Sempre que você usar funções de inteligência de tempo DAX, como quando você cria medidas mais adiante, você deve especificar as propriedades que inclui um *tabela de datas* e um identificador exclusivo *coluna data* nessa tabela.
  
Nesta lição, você deve marcar a **DimDate** de tabela como o *a tabela de data* e o **data** coluna (na tabela de data) como o *coluna data* (exclusivo identificador).  

Antes de marcar a tabela de data e a coluna de data, é um bom momento para fazer uma pequena limpeza para facilitar a compreensão do seu modelo. Observe, na tabela DimDate, uma coluna denominada **FullDateAlternateKey**. Esta coluna contém uma linha para cada dia em cada ano civil incluído na tabela. Você usa muito essa coluna em fórmulas de medida e em relatórios. Mas, FullDateAlternateKey não é um bom identificador para essa coluna. Você renomeá-lo para **data**, tornando mais fácil de identificar e incluir em fórmulas. Sempre que possível, é uma boa ideia para renomear objetos, como tabelas e colunas para torná-los mais fáceis de identificar no SSDT e aplicativos cliente de relatório. 
  
Tempo estimado para concluir esta lição: **três minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 2: obter dados](../tutorial-tabular-1400/as-lesson-2-get-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para renomear a coluna FullDateAlternateKey

1.  No designer de modelo, clique o **DimDate** tabela.

2.  Clique duas vezes no cabeçalho para o **FullDateAlternateKey** coluna e, em seguida, renomeie-o como **data**.

  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  Selecione a coluna **Data** e, na janela **Propriedades** , em **Tipo de Dados**, verifique se a opção  **Data** está selecionada.  
  
2.  Clique no menu **Tabela** , clique em **Data**e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo. Ela geralmente é selecionada por padrão. Clique em **OK**. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 4: Criar relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md).
  
