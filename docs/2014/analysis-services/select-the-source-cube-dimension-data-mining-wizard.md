---
title: Selecionar a dimensão do cubo de origem (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdb61763a49bad7eae1a49a01633ec8f45e27642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069226"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>Selecionar a dimensão do cubo de origem (Assistente de Mineração de Dados)
  Use a página **Selecionar a Dimensão do Cubo de Origem** para selecionar a dimensão do cubo que contém os casos a serem analisados. Por exemplo, se você estiver criando um modelo que analise o comportamento de compra dos clientes com base em dados demográficos, selecione a dimensão Cliente, que em geral contém um registro exclusivo para cada cliente e vários atributos que representam dados demográficos, como sexo, local ou renda. Posteriormente no assistente, você terá a oportunidade de adicionar uma tabela relacionada a essa tabela de casos: por exemplo, você pode adicionar uma tabela aninhada que mostre quais produtos o cliente comprou.  
  
> [!NOTE]  
>  Essa página será exibida apenas se você tiver selecionado **De cubo existente** na página **Selecionar o Método de Definição** do assistente.  
  
## <a name="options"></a>Opções  
 **Selecione uma dimensão de cubo de origem**  
 Selecione a dimensão do cubo que fornecerá os dados de origem para sua estrutura de mineração.  
  
## <a name="choosing-a-dimension"></a>Escolhendo uma dimensão  
 Como você pode selecionar apenas uma dimensão para uso no modelo, é importante entender a estrutura do cubo e selecionar a dimensão que fornece as melhores informações para o modelo. Se você não tiver certeza em relação a qual dimensão usar, talvez seja útil percorrer o cubo e examinar os campos e os dados nele usando o Designer de Dimensão. Para obter mais informações, consulte [Procurar dados de dimensão no Designer de Dimensão](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md).  
  
 Se não estiver familiarizado com as dimensões em geral, consulte [Introdução a Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Para saber mais sobre o tipo de informações geralmente contidas em uma única dimensão, incluindo os atributos e as medidas que podem ser úteis para mineração de dados, consulte [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Se a dimensão escolhida não contiver todos os atributos relacionados necessários para criar o modelo de mineração de dados, talvez seja necessário modificá-la. Para obter mais informações, consulte [Definir as dimensões do banco de dados](multidimensional-models/define-database-dimensions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Criar a estrutura de mineração de dados &#40;Assistente de mineração de dados&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [Selecione a chave do caso &#40;Assistente de mineração de dados&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
