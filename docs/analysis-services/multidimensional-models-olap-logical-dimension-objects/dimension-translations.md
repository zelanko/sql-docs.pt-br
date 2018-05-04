---
title: Traduções da dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8fbaaf3619b5a359de71299d1e5246e5670d5d7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-translations"></a>Tradução de dimensões
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma tradução é um mecanismo simples para alterar os rótulos e legendas exibidos de um idioma para outro. Cada tradução é definida como um par de valores: uma cadeia de caracteres com o texto traduzido e um número com uma ID do idioma. As traduções estão disponíveis para todos os objetos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. As dimensões também podem ter os valores de atributo traduzidos. O aplicativo cliente é responsável por encontrar a configuração de idioma que o usuário definiu e alternar a exibição de todas as legendas e rótulos para esse idioma. Um objeto pode ter a quantidade de traduções que você desejar.  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Translation> é composto de: número de ID do idioma e legenda traduzida. O número de ID de idioma é um **inteiro** com a ID de idioma. A legenda traduzida é o texto traduzido.  
  
 Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma tradução de dimensão é uma representação de específico do idioma do nome da dimensão, o nome de uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto ou um de seus membros, como um legenda, membro ou nível hierárquico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também oferece suporte a traduções de objetos de cubo.  
  
 As traduções oferecem suporte de servidor a aplicativos cliente que podem oferecer suporte para vários idiomas. Frequentemente, os usuários de países diferentes exibem um cubo e suas dimensões. É útil poder traduzir vários elementos de um cubo e suas dimensões em um idioma diferente, de modo que esses usuários possam exibir e compreender o cubo. Por exemplo, um usuário empresarial na França pode acessar um cubo a partir de uma estação de trabalho com uma configuração de localidade francesa e visualizar os valores de propriedade do objeto em francês. Entretanto, um usuário empresarial na Alemanha que acessa o mesmo cubo a partir de uma estação de trabalho com uma configuração de localidade alemã, visualiza os mesmos valores de propriedade do objeto em alemão.  
  
 As informações de agrupamento e idioma para o computador cliente são armazenadas na forma de um LCID (identificador de localidade). Em conexão, o cliente passa o LCID à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A instância usa o LCID para determinar qual conjunto de traduções será usado para fornecer metadados aos objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não contiver a tradução especificada, o idioma padrão será usado para retornar o conteúdo de volta ao cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Traduções de cubo](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Suporte a tradução no Analysis Services](../../analysis-services/translation-support-in-analysis-services.md)   
 [Dicas de globalização e práticas recomendadas & #40; Analysis Services & #41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
