---
title: 'Lição 4: Marcar como tabela de data | Microsoft Docs'
ms.custom: ''
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 08a3e1852f58e1f21049d1a5c0551669423845db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-mark-as-date-table"></a>Lição 3: Marcar como tabela de data
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Na lição 2: Adicionar Dados, você importou uma tabela de dimensão chamada DimDate. Enquanto seu modelo essa tabela é denominada DimDate, ele também é conhecido como uma *a tabela de data*, em que ela contém dados de data e hora.  
  
Sempre que você usa funções de inteligência de tempo DAX em cálculos, como fará quando você cria medidas mais adiante, você deve especificar as propriedades de tabela de data, que incluem um *a tabela de data* e um identificador exclusivo *data coluna* nessa tabela.
  
Nesta lição, você poderá marcar a tabela de DimDate como o *a tabela de data* e a coluna de data (na tabela de data) como o *coluna data* (identificador exclusivo).  

Antes, marcar a tabela de data e a coluna de data, precisamos fazer um pouco manutenção do sistema para facilitar a compreensão de nosso modelo. Você observará na tabela DimDate uma coluna denominada **FullDateAlternateKey**. Ele contém uma linha para cada dia em cada ano civil incluído na tabela. Usaremos essa coluna muito em fórmulas de medida e nos relatórios. Porém, FullDateAlternateKey não é realmente um identificador válido para essa coluna. Iremos renomear a **data**, tornando mais fácil identificar e incluir em fórmulas. Sempre que possível, é recomendável renomear objetos, como tabelas e colunas para torná-los mais fáceis de identificar no cliente de relatório de aplicativos, como o Power BI e Excel. 
  
Tempo estimado para concluir esta lição: **3 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 2: adicionar dados](../analysis-services/lesson-2-add-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para renomear a coluna FullDateAlternateKey

1.  No designer de modelo, clique o **DimDate** tabela.

2.  Clique duas vezes no cabeçalho para o **FullDateAlternateKey** coluna e, em seguida, renomeie-o para **data**.

  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  Selecione a coluna **Data** e, na janela **Propriedades** , em **Tipo de Dados**, verifique se a opção  **Data** está selecionada.  
  
2.  Clique no menu **Tabela** , clique em **Data**e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo. Normalmente, ela será selecionada por padrão. Clique em **OK**. 

    ![como tabular-Lição3-data-tabela](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 4: criar relações](../analysis-services/lesson-4-create-relationships.md).
  
