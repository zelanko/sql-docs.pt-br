---
title: 'Lição 3 do tutorial de serviços de análise: marcar como tabela de data | Microsoft Docs'
description: Descreve como marcar uma tabela de data no projeto do tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8d15495ef5c1fdfe4150990f5ca24e022b4fe05a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mark-as-date-table"></a>Marcar como Tabela de Data

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Na lição 2: Obter dados, você importou uma tabela de dimensão chamada **DimDate**. Enquanto seu modelo essa tabela é denominada DimDate, ele também é conhecido como uma *a tabela de data*, em que ela contém dados de data e hora.  
  
Sempre que você usar funções de inteligência de tempo DAX, como quando você criar medidas mais tarde, você deve especificar as propriedades que incluem um *a tabela de data* e um identificador exclusivo *coluna data* nessa tabela.
  
Nesta lição, você deve marcar o **DimDate** tabela como o *a tabela de data* e **data** coluna (na tabela de data) como o *coluna data* (exclusivo identificador).  

Antes de marcar a tabela de data e a coluna de data, é um bom momento para fazer a manutenção do sistema um pouco para facilitar a compreensão do seu modelo. Observe, na tabela DimDate, uma coluna denominada **FullDateAlternateKey**. Esta coluna contém uma linha para cada dia em cada ano civil incluído na tabela. Você usa essa coluna muito em fórmulas de medida e em relatórios. Porém, FullDateAlternateKey não é um identificador válido para essa coluna. Você renomeá-la para **data**, tornando mais fácil identificar e incluir em fórmulas. Sempre que possível, é recomendável renomear objetos, como tabelas e colunas para torná-los mais fáceis de identificar no SSDT e aplicativos cliente de relatório. 
  
Tempo estimado para concluir esta lição: **três minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 2: obter dados](../tutorial-tabular-1400/as-lesson-2-get-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para renomear a coluna FullDateAlternateKey

1.  No designer de modelo, clique o **DimDate** tabela.

2.  Clique duas vezes no cabeçalho para o **FullDateAlternateKey** coluna e, em seguida, renomeie-o para **data**.

  
### <a name="to-set-mark-as-date-table"></a>Para definir Marcar como Tabela de Data  
  
1.  Selecione a coluna **Data** e, na janela **Propriedades** , em **Tipo de Dados**, verifique se a opção  **Data** está selecionada.  
  
2.  Clique no menu **Tabela** , clique em **Data**e em **Marcar como Tabela de Data**.  
  
3.  Na caixa de diálogo **Marcar como Tabela de Data** , na caixa de listagem **Data** , selecione a coluna **Data** como o identificador exclusivo. Ele geralmente é selecionado por padrão. Clique em **OK**. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 4: Criar relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md).
  
