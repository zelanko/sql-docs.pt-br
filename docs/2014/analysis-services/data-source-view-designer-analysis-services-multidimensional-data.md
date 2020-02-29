---
title: Designer de exibição da fonte de dados (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd19f3a7f4978d2f8bcbd8e62cdf542e05437519
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175162"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>Designer de Exibição da Fonte de Dados (Analysis Services – Dados Multidimensionais)
  Uma exibição da fonte de dados (DSV) é uma exibição lógica de uma fonte de dados relacional externa usada para criar cubos e dimensões em um modelo multidimensional.

 Depois que um DSV é gerado, você pode usar o **Designer de Exibição da Fonte de Dados** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para trabalhar diretamente no DSV, o que pode ser útil se a fonte de dados subjacente não tiver elementos de dados necessários em um modelo multidimensional.

 Para abrir o **Designer de Exibição da Fonte de Dados** :

-   Clique duas vezes em uma exibição de fonte de dados no **Gerenciador de Soluções**.

-   Clique com o botão direito do mouse em uma exibição da fonte de dados no **Gerenciador de Soluções** e selecione **Abrir** ou **Designer de Exibição**.

 O **Designer de Exibição da Fonte de Dados** contém uma barra de ferramentas, um diagrama que mostra os objetos e as relações no DSV, um painel de tabelas listando tabelas e consultas nomeadas em ordem alfabética e um painel Organizador de Diagramas usado para criar e exibir diagramas específicos do DSV. Clique com o botão direito na tabela ou relacionamento para acessar comandos de contexto.

 ![Designer de Exibição da Fonte de Dados](media/ssas-dsvdesigner.PNG "Designer de Exibição da Fonte de Dados")

 No mínimo, um DSV mostra as tabelas de banco de dados relacional que serão usadas para popular objetos de modelo durante o processamento. Um DSV é gerado, geralmente usando o assistente da Exibição da Fonte de Dados. As tabelas, as colunas e os relacionamentos no DSV tornam-se a base para dimensões e medidas em um cubo. Quando o DSV é criado, você pode usar o Designer de Exibição da Fonte de Dados para modificá-lo.

 A maioria dos desenvolvedores do Analysis Services usam um DSV gerado no estado, com poucas personalizações. Isso é especialmente comum se os dados de origem são originados de uma exibição em um banco de dados do SQL Server. Nesse caso, você pode preferir gerenciar relacionamentos de dados e cálculos em uma exibição de T-SQL em vez de um DSV do Analysis Services. No entanto, se você não for o proprietário do banco de dados subjacente, poderá alterar o DSV no Analysis Services para desenvolver mais as estruturas de dados usadas em seu modelo.

## <a name="tasks-in-data-source-view-designer"></a>Tarefas no Designer de Exibição da Fonte de Dados
 Usando o Designer de Exibição da Fonte de Dados, você pode fazer as seguintes edições em um DSV:

|||
|-|-|
|Renomear colunas ou tabelas ou criar novas colunas calculadas. Por exemplo, concatene um nome e sobrenome em uma nova coluna de nome completo.|[Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|
|Adicionar manualmente relacionamentos de tabela|[Definir relações lógicas em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|
|Crie uma consulta nomeada para definir um novo objeto com base em uma consulta T-SQL genérica.|[Definir consultas nomeadas em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|
|Explore os dados subjacentes para exibir os valores de dados reais representados por objetos de modelo.<br /><br /> A exploração de dados permite a você inspecionar visualmente e copiar dados retornados da tabela dimensional ou consulta dimensional subjacente. Por padrão, a exploração de dados usa a metodologia de amostragem de contagem superior, com uma contagem de exemplo de 5000, mas você pode revisar essas configurações.|[Explorar dados em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|
|Diagrame todas ou parte das tabelas e relacionamentos em um DSV|[Trabalhar com diagramas no designer de exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|

## <a name="see-also"></a>Consulte Também
 [Exibições da fonte de dados em modelos multidimensionais](multidimensional-models/data-source-views-in-multidimensional-models.md) [adicionando ou removendo tabelas ou exibições em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)


