---
title: Conversões de cubo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- cubes [Analysis Services], translations
- OLAP objects [Analysis Services], translations
- translations [Analysis Services], cubes
ms.assetid: 4e4fd6a4-d324-4508-b75a-2a57de9ab8ff
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c34024f61f5c7b42030e0acb848783e1acae3d6e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62728490"
---
# <a name="cube-translations"></a>Traduções de cubo
  Uma tradução é um mecanismo simples para alterar os rótulos e legendas exibidos de um idioma para outro. Cada tradução é definida como um par de valores: uma cadeia de caracteres com o texto traduzido e um número com uma ID do idioma. As traduções estão disponíveis para todos os objetos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. As dimensões também podem ter os valores de atributo traduzidos. O aplicativo cliente é responsável por encontrar a configuração de idioma que o usuário definiu e alternar a exibição de todas as legendas e rótulos para esse idioma. Um objeto pode ter a quantidade de traduções que você desejar.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Translation> é composto de: número de ID do idioma e legenda traduzida. O número de ID do idioma é um `Integer` com uma ID do idioma. A legenda traduzida é o texto traduzido.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma tradução de cubo é uma representação específica do idioma do nome de um objeto de cubo, como uma legenda ou uma pasta de exibição. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também oferece suporte às traduções de nomes de membros da dimensão.  
  
 As traduções oferecem suporte de servidor a aplicativos cliente que podem oferecer suporte para vários idiomas. Frequentemente, usuários de países diferentes exibem dados de cubo. É útil poder de traduzir vários elementos de um cubo em um idioma diferente de modo que esses usuários possam exibir e compreender os metadados do cubo. Por exemplo, um usuário empresarial na França pode acessar um cubo a partir de uma estação de trabalho com uma configuração de localidade francesa e exibir os valores de propriedade do objeto em francês. Do mesmo modo, um usuário empresarial na Alemanha pode acessar o mesmo cubo a partir de uma estação de trabalho com uma configuração de localidade alemã e exibir os valores de propriedade do objeto em alemão.  
  
 As informações de ordenação e idioma para o computador cliente são armazenadas na forma de um LCID (identificador de localidade). Em conexão, o cliente passa o LCID à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A instância usa o LCID para determinar qual conjunto de traduções será usado para fornecer metadados aos objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para cada usuário empresarial. Se um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não contiver a tradução especificada, o idioma padrão será usado para retornar o conteúdo de volta ao cliente.  
  
## <a name="see-also"></a>Consulte Também  
 [Traduções de dimensão](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Conversões &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
