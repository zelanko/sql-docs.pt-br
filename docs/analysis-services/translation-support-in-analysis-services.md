---
title: Suporte a tradução no Analysis Services | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd727b56649ce9ffc237575b0311db256ec9b2fc
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54184922"
---
# <a name="translation-support-in-analysis-services"></a>Suporte a tradução no Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] modelos de dados, você pode inserir várias traduções de uma legenda ou uma descrição para fornecer cadeias de caracteres específicas da cultura com base no identificador de localidade (LCID). Para modelos multidimensionais, as traduções podem ser adicionadas para o nome do banco de dados, objetos de cubo e objetos de dimensão do banco de dados. Para modelos de tabela, você pode traduzir descrições e legendas de tabela e coluna.  
  
 A definição de uma tradução cria os metadados e legenda traduzida dentro do modelo, mas para renderizar cadeias de caracteres localizadas em um aplicativo cliente, você deverá definir a propriedade **Language** no objeto ou passar um parâmetro **Culture** ou **Locale Identifier** na cadeia de conexão (por exemplo, definindo `LocaleIdentifier=1036` para retornar cadeias de caracteres em francês).  
  
 Planeje o uso de **Locale Identifier** se desejar dar suporte a várias traduções simultâneas do mesmo objeto em idiomas diferentes. Definir a propriedade **Language** funciona, mas isso também afeta o processamento e as consultas, o que pode ter consequências indesejadas. Definir **Locale Identifier** é a melhor opção porque ele é usado somente para retornar cadeias de caracteres traduzidas.  
  
 Uma tradução consiste em um identificador de localidade (LCID), uma legenda traduzida para o objeto (por exemplo, a dimensão ou o nome do atributo) e, opcionalmente, uma associação a uma coluna que fornece valores de dados no idioma de destino. Você pode ter várias traduções, mas só pode usar uma para determinada conexão. Não há nenhum limite teórico no número de traduções que você pode inserir no modelo, mas cada tradução adiciona complexidade ao teste e todas as traduções devem compartilhar a mesma ordenação, portanto, ao criar a solução, lembre-se dessas restrições naturais.  
  
> [!TIP]  
>  Você pode usar os aplicativos cliente, como Excel, SQL Server Management Studio e SQL Server Profiler para retornar cadeias de caracteres traduzidas. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>Como adicionar metadados traduzidos para o modelo no Analysis Services  
 Visite esses links para obter instruções passo a passo:  
  
-   [Traduções em modelos de tabela](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [Traduções em modelos multidimensionais](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>Confira também  
 [Cenários de globalização para o Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Idiomas e ordenações &amp;#40;Analysis Services&amp;#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [Definir ou alterar a ordenação de coluna](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
