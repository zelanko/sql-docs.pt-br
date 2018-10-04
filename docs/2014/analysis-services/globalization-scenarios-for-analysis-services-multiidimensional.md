---
title: Cenários de globalização para Analysis Services multidimensional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e88100d935898e69ac924ecb5a44ee562079e0dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063096"
---
# <a name="globalization-scenarios-for-analysis-services-multiidimensional"></a>Cenários de globalização para Analysis Services Multidimensional
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] armazena e manipula dados multilíngues e metadados em ambos os modelos de dados multidimensionais e tabulares. O armazenamento de dados é Unicode (UTF-16), em conjuntos de caracteres que usam a codificação Unicode. Se você carregar dados ANSI em um modelo de dados, os caracteres são armazenados usando pontos de código equivalentes a Unicode.  
  
 As implicações do suporte a Unicode significam que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode armazenar dados em qualquer uma das linguagens com suporte pelo cliente e servidor de sistemas operacionais Windows, permissão de leitura, gravação, classificação e comparação de dados em qualquer conjunto de caracteres usado em um computador Windows. Aplicativos clientes de BI que consomem dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podem representar dados no idioma de preferência do usuário, supondo que os dados encontram-se no mesmo idioma do modelo.  
  
 Suporte a idiomas pode significar coisas diferentes para pessoas diferentes. A lista a seguir aborda algumas perguntas comuns relacionadas a como o Analysis Services dá suporte a idiomas.  
  
-   Dados, como já observados, são armazenados em qualquer conjunto de caracteres codificado com Unicode encontrado no sistema operacional do cliente Windows.  
  
-   Metadados, como nomes de objeto, identificadores e descrições, também podem estar em qualquer linguagem e script Unicode. Isso é verdadeiro mesmo quando as ferramentas e o ambiente estão em outro idioma. Por exemplo, em um ambiente de desenvolvimento que usa o idioma inglês e um agrupamento latino em toda a pilha, você pode incluir em seu modelo de um objeto que usa caracteres cirílicos no nome.  
  
     Para modelos multidimensionais apenas, legendas e membros de atributo podem ser expressos como traduções. Você pode definir uma ou mais traduções e, em seguida, usar um identificador de localidade para determinar qual tradução é retornada ao cliente. Consulte [Recursos](#bkmk_features) abaixo para mais detalhes.  
  
-   Erro, aviso e mensagens informativas retornadas do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] mecanismo (msmdsrv) estão localizados nos 43 idiomas com suporte pelo Office e Office 365. Nenhuma configuração é necessária para receber mensagens em um idioma específico. A localidade do aplicativo cliente determina quais cadeias de caracteres são retornadas.  
  
-   O arquivo de configuração (msmdsrv) e AMO PowerShell estão disponíveis apenas em inglês.  
  
-   Os arquivos de log conterão uma mistura mensagens em inglês e traduzidas, supondo que você instalou um pacote de idiomas no servidor Windows que executa o Analysis Services.  
  
-   Documentos e ferramentas, tais como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)], estão traduzidos para os seguintes idiomas: chinês simplificado, chinês tradicional, francês, alemão, italiano, japonês, coreano, português (Brasil), russo e espanhol. Para usar uma versão específica do idioma das ferramentas, instale uma versão de linguagem específica do SQL Server (por exemplo, instalar a versão em alemão do SQL Server para obter o Management Studio em alemão) ou execute a instalação autônoma no idioma de destino para [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)].  
  
 O Analysis Services permite definir idioma, agrupamento e traduções de forma independente em toda a hierarquia de objetos.  
  
 Os cenários habilitados por meio da linguagem, agrupamentos e traduções incluem:  
  
-   Um modelo de dados fornece várias legendas traduzidas para que os valores e nomes de campos sejam exibidos no idioma de preferência do usuário. Para empresas que operam em países bilíngues como Suíça, Bélgica ou no Canadá, o suporte a vários idiomas em aplicativos cliente e servidor é um requisito padrão de codificação. Este cenário é habilitado por meio de traduções e conversões de moeda. Consulte [Recursos](#bkmk_features) abaixo para obter detalhes e links.  
  
-   Ambientes de desenvolvimento e produção estão localizados geograficamente em diferentes países. É cada vez mais comum desenvolver uma solução em um país e, em seguida, implantá-la em outro. Saber como definir as propriedades de agrupamento e idioma é essencial se você ficar encarregado de preparar uma solução desenvolvida em um idioma para implantação em um servidor que usa um pacote de idiomas diferente. A configuração dessas propriedades permite substituir os padrões herdados que você obtém do sistema host original. Consulte [Languages and Collations &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md) para obter detalhes sobre como definir propriedades.  
  
##  <a name="bkmk_features"></a> Recursos para a criação de uma solução multidimensional globalizada  
 [!INCLUDE[applies](../includes/applies-md.md)] Somente modelos de dados multidimensionais  
  
 No nível do cliente, aplicativos globalizados que consomem ou manipulam [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dados multidimensionais podem usar os recursos multilíngues e multiculturais no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
-   [Traduções &#40;Analysis Services&#41; ](translations-analysis-services.md) são usados para inserir várias legendas em um único objeto, onde cada cadeia traduzida pode coexistir com outras traduções. Você pode usar [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir as traduções da legenda, descrição e tipos de conta para cubos e medidas, dimensão e atributos. É possível recuperar dados e metadados de objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nos quais foram definidas traduções automaticamente, fornecendo um identificador de localidade ao se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
     Uma lição sobre como usar esse recurso pode ser encontrada na [Lição 9: definindo perspectivas e traduções](lesson-9-defining-perspectives-and-translations.md) do tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   [Conversões de moeda &#40;Analysis Services&#41; ](currency-conversions-analysis-services.md) é por meio de scripts MDX especializados que convertem medidas contendo dados de moeda. Você pode usar o Assistente de Business Intelligence em [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] para gerar um script MDX que usa uma combinação de dados e metadados de dimensões, atributos e grupos de medidas para converter medidas contendo dados de moeda.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Idiomas e agrupamentos &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)|Especifique o idioma padrão e agrupamento do Windows para uma instância [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Suas escolhas afetam dados e metadados gerenciados pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|[Traduções &#40;Analysis Services&#41;](translations-analysis-services.md)|Definir traduções para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados e objetos contidos pelo banco de dados. Este tópico explica como o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] resolve solicitações de dados traduzidos e metadados de aplicativos cliente.|  
|[Conversões de moeda &#40;Analysis Services&#41;](currency-conversions-analysis-services.md)|Definir uma conversão de moeda usando o Assistente de Business Intelligence.|  
|[Dicas de globalização e práticas recomendadas para o &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)|Examina várias práticas de design e codificação que podem ajudá-lo a evitar problemas relacionados a dados em vários idiomas.|  
  
## <a name="see-also"></a>Consulte também  
 [Internacionalização para aplicativos do Windows](/windows/desktop/Intl/international-support)   
 [Go Global Developer Center](http://msdn.microsoft.com/goglobal/bb871628.aspx)   
 [Aplicativos de gravação Windows Store com design adaptável baseado em localidade](http://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [Desenvolvimento de aplicativos Universal do Windows com c# e XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
