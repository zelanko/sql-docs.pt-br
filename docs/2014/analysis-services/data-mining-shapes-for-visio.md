---
title: Formas de mineração de dados para o Visio | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ebe206d4f4942e9a9456ba10b00d33514ef6212
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086402"
---
# <a name="data-mining-shapes-for-visio"></a>Formas de mineração de dados para o Visio
  As Formas de Mineração de Dados para o Visio fornecem modelos personalizados para exibir modelos de mineração de dados. Usando esses modelos, é possível se conectar a um modelo que você criou, e criar apresentações interativas para ilustrar os resultados da mineração de dados.  
  
 Os modelos oferecem muitas vantagens sobre grafos estáticos e capturas de tela – eles interagem com os modelos de Data Mining subjacentes, que são armazenados em uma instância do Analysis Services e permitem que você personalize a maneira como os padrões no modelo de mineração são exibidos. Você pode recolher e expandir um modelo de árvore, filtrar os nós de dados ou por atributos e exibir estatísticas de modelo como probabilidades e coeficientes.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Os modelos do Visio incluem estes assistentes:  
  
-   **Diagrama de rede de dependência:** Use este assistente para criar grafos para árvores de decisão e redes neurais.  
  
-   **Diagrama de árvore de decisão:** Use este assistente para criar diagramas que mostram os pontos de decisão e as fórmulas associados aos modelos de árvore de decisão. Esse diagrama também pode ser usado com modelos de regressão.  
  
-   **Diagrama de cluster:** Use este assistente para criar grafos coloridos para seus modelos de segmentação. Você pode alternar entre exibições como distinção de atributo, perfis de cluster e dependências, e personalizar a aparência de clusters.  
  
## <a name="installation"></a>Instalação  
 Quando você instala os modelos de mineração de dados para o Visio, por padrão, os arquivos \<a seguir são instalados na unidade> \program Files\Microsoft SQL Server 2012 DM \<Add-ins (ou drive> ou arquivos de programas (x86) \Microsoft SQL Server 2012 DM Add-ins):  
  
-   **Mineração de dados da Microsoft. VST** Este modelo contém formatação, layout e assistentes predefinidos para ajudá-lo a trabalhar com as formas de Data Mining.  
  
-   **Microsoft Data Mining Shape Studio. VSS** Este arquivo de estêncil contém formas associadas ao modelo.  
  
## <a name="how-to-use-the-templates"></a>Como usar os modelos  
 Para abrir os modelos, você pode clicar duas vezes no arquivo de forma ou pode abrir o Visio e o modelo de forma.  
  
1.  Descarte uma das formas de mineração de dados do Visio do estêncil em uma nova página.  
  
2.  Quando o assistente for iniciado, conecte-se ao servidor que tem o modelo de mineração de dados a ser exibido.  
  
3.  Selecione o modelo de mineração de dados, correspondendo o tipo de modelo ao tipo de visualização.  
  
4.  Defina as opções de como os dados devem ser exibidos e formatados.  
  
5.  Depois de concluir o **Assistente de forma de mineração de dados**, você tem um diagrama que pode ser modificado e aprimorado usando os recursos do Visio.  
  
 Para obter mais informações sobre como trabalhar com e aprimorar diagramas de modelo do Visio, consulte [exibindo modelos de mineração de dados no Visio &#40;suplementos de mineração de dados&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>Requisitos  
  
-   Para usar os modelos, primeiro crie uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
     O assistente solicitará que você selecione um servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e especifique o banco de dados que contém o modelo de mineração.  
  
     Para obter informações sobre como criar uma conexão, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
-   Se você estiver usando as Ferramentas de Análise de Tabela, verifique se salvou os modelos no servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], e não use modelos temporários.  
  
-   O modelo deve ter sido criado usando um dos algoritmos com suporte: clustering, árvores de decisão, redes neurais, Naïve Bayes ou regressão logística.  
  
  
