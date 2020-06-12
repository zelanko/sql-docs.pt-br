---
title: Traduções de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6f31773ad871ef7e3fc8f99d57e7a9099335b899
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545143"
---
# <a name="dimension-translations"></a>Tradução de dimensões
  Uma tradução é um mecanismo simples para alterar os rótulos e legendas exibidos de um idioma para outro. Cada tradução é definida como um par de valores: uma cadeia de caracteres com o texto traduzido e um número com uma ID do idioma. As traduções estão disponíveis para todos os objetos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. As dimensões também podem ter os valores de atributo traduzidos. O aplicativo cliente é responsável por encontrar a configuração de idioma que o usuário definiu e alternar a exibição de todas as legendas e rótulos para esse idioma. Um objeto pode ter a quantidade de traduções que você desejar.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Translation> é composto de: número de ID do idioma e legenda traduzida. O número de ID do idioma é um `Integer` com uma ID do idioma. A legenda traduzida é o texto traduzido.  
  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , uma conversão de dimensão é uma representação específica do idioma do nome de uma dimensão, o nome de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto ou um de seus membros, como uma legenda, um membro ou um nível de hierarquia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]também oferece suporte a traduções de objetos de cubo.  
  
 As traduções oferecem suporte de servidor a aplicativos cliente que podem oferecer suporte para vários idiomas. Frequentemente, os usuários de países diferentes exibem um cubo e suas dimensões. É útil poder traduzir vários elementos de um cubo e suas dimensões em um idioma diferente, de modo que esses usuários possam exibir e compreender o cubo. Por exemplo, um usuário empresarial na França pode acessar um cubo a partir de uma estação de trabalho com uma configuração de localidade francesa e visualizar os valores de propriedade do objeto em francês. Entretanto, um usuário empresarial na Alemanha que acessa o mesmo cubo a partir de uma estação de trabalho com uma configuração de localidade alemã, visualiza os mesmos valores de propriedade do objeto em alemão.  
  
 As informações de ordenação e idioma para o computador cliente são armazenadas na forma de um LCID (identificador de localidade). Em conexão, o cliente passa o LCID à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A instância usa o LCID para determinar qual conjunto de traduções será usado para fornecer metadados aos objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não contiver a tradução especificada, o idioma padrão será usado para retornar o conteúdo de volta ao cliente.  
  
## <a name="see-also"></a>Consulte Também  
 [Traduções de cubo](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Conversões &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
