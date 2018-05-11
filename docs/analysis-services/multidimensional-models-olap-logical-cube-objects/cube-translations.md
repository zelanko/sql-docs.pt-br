---
title: Traduções de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eed8fb8bed88ae3358cb30a0c8913f3275367f9a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="cube-translations"></a>Traduções de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma tradução é um mecanismo simples para alterar os rótulos e legendas exibidos de um idioma para outro. Cada tradução é definida como um par de valores: uma cadeia de caracteres com o texto traduzido e um número com uma ID do idioma. As traduções estão disponíveis para todos os objetos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. As dimensões também podem ter os valores de atributo traduzidos. O aplicativo cliente é responsável por encontrar a configuração de idioma que o usuário definiu e alternar a exibição de todas as legendas e rótulos para esse idioma. Um objeto pode ter a quantidade de traduções que você desejar.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Translation> é composto de: número de ID do idioma e legenda traduzida. O número de ID de idioma é um **inteiro** com a ID de idioma. A legenda traduzida é o texto traduzido.  
  
 Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma tradução de cubo é uma representação de específico do idioma do nome de um objeto de cubo, como uma legenda ou uma pasta de exibição. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também oferece suporte às traduções de nomes de membros da dimensão.  
  
 As traduções oferecem suporte de servidor a aplicativos cliente que podem oferecer suporte para vários idiomas. Frequentemente, usuários de países diferentes exibem dados de cubo. É útil poder de traduzir vários elementos de um cubo em um idioma diferente de modo que esses usuários possam exibir e compreender os metadados do cubo. Por exemplo, um usuário empresarial na França pode acessar um cubo a partir de uma estação de trabalho com uma configuração de localidade francesa e exibir os valores de propriedade do objeto em francês. Do mesmo modo, um usuário empresarial na Alemanha pode acessar o mesmo cubo a partir de uma estação de trabalho com uma configuração de localidade alemã e exibir os valores de propriedade do objeto em alemão.  
  
 As informações de agrupamento e idioma para o computador cliente são armazenadas na forma de um LCID (identificador de localidade). Em conexão, o cliente passa o LCID à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A instância usa o LCID para determinar qual conjunto de traduções será usado para fornecer metadados aos objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para cada usuário empresarial. Se um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não contiver a tradução especificada, o idioma padrão será usado para retornar o conteúdo de volta ao cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Conversões de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Suporte a tradução no Analysis Services](../../analysis-services/translation-support-in-analysis-services.md)   
 [Dicas de globalização e práticas recomendadas & #40; Analysis Services & #41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
