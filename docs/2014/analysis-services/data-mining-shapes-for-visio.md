---
title: Formas de mineração de dados para Visio | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cd037e0d4eefb7f894d956222219902a5082fffd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008517"
---
# <a name="data-mining-shapes-for-visio"></a>Formas de mineração de dados para o Visio
  As Formas de Mineração de Dados para o Visio fornecem modelos personalizados para exibir modelos de mineração de dados. Usando esses modelos, é possível se conectar a um modelo que você criou, e criar apresentações interativas para ilustrar os resultados da mineração de dados.  
  
 Os modelos oferecem muitas vantagens em relação aos gráficos estáticos e às capturas de tela – eles interagem com os modelos de mineração de dados subjacente, que são armazenados em uma instância do Analysis Services, e permitem personalizar a forma como os padrões no modelo de mineração são exibidos. Você pode recolher e expandir um modelo de árvore, filtrar os nós de dados ou por atributos e exibir estatísticas de modelo como probabilidades e coeficientes.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Os modelos do Visio incluem estes assistentes:  
  
-   **Diagrama de rede de dependência:** Use este assistente para criar gráficos para árvores de decisão e redes neurais.  
  
-   **Diagrama de árvore de decisão:** Use este assistente para criar diagramas que mostram os pontos de decisão e as fórmulas associadas à árvore de decisão. Esse diagrama também pode ser usado com modelos de regressão.  
  
-   **Diagrama de cluster:** Use este assistente para criar gráficos coloridos para seus modelos de segmentação. Você pode alternar entre exibições como distinção de atributo, perfis de cluster e dependências, e personalizar a aparência de clusters.  
  
## <a name="installation"></a>Instalação  
 Quando você instala os modelos de mineração de dados para Visio, por padrão os seguintes arquivos são instalados para \<drive > \Program Files\Microsoft SQL Server 2012 DM Add-Ins (ou \<unidade > \ ou arquivos de programa (x86) \Microsoft SQL Server 2012 DM Add-Ins):  
  
-   **Microsoft Data Mining.vst** este modelo contém formatação predefinida, layout e assistentes para ajudá-lo a trabalhar com as formas de mineração de dados.  
  
-   **Microsoft Data Mining Shape Studio.vss** esse arquivo de estêncil contém formas associadas ao modelo.  
  
## <a name="how-to-use-the-templates"></a>Como usar os modelos  
 Para abrir os modelos, você pode clicar duas vezes no arquivo de forma ou pode abrir o Visio e o modelo de forma.  
  
1.  Descarte uma das formas de mineração de dados do Visio do estêncil em uma nova página.  
  
2.  Quando o assistente for iniciado, conecte-se ao servidor que tem o modelo de mineração de dados a ser exibido.  
  
3.  Selecione o modelo de mineração de dados, correspondendo o tipo de modelo ao tipo de visualização.  
  
4.  Defina as opções de como os dados devem ser exibidos e formatados.  
  
5.  Depois de concluir o **Assistente de formas de mineração de dados**, você tem um diagrama que você pode modificar e aprimorar usando os recursos do Visio.  
  
 Para obter mais informações sobre como trabalhar com e aprimorar diagramas de modelo do Visio, consulte [exibindo modelos de mineração de dados no Visio &#40;suplementos de mineração de dados&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>Requisitos  
  
-   Para usar os modelos, primeiro crie uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
     O assistente solicitará que você selecione um servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e especifique o banco de dados que contém o modelo de mineração.  
  
     Para obter informações sobre como criar uma conexão, consulte [conectar-se à fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
-   Se você estiver usando as Ferramentas de Análise de Tabela, verifique se salvou os modelos no servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], e não use modelos temporários.  
  
-   O modelo deve ter sido criado usando um dos algoritmos com suporte: clustering, árvores de decisão, redes neurais, Naïve Bayes ou regressão logística.  
  
  