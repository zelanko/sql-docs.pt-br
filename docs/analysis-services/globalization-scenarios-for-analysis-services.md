---
title: Cenários de globalização para Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4cfbb4d3cfb62405546ef5ff955a52811ded41b5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202245"
---
# <a name="globalization-scenarios-for-analysis-services"></a>Cenários de globalização para o Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] armazena e manipula dados multilíngues e metadados tanto nos modelos de dados tabulares quanto nos multidimensionais. O armazenamento de dados é Unicode (UTF-16), em conjuntos de caracteres que usam a codificação Unicode. Se você carregar dados ANSI em um modelo de dados, os caracteres são armazenados usando pontos de código equivalentes a Unicode.  
  
 As implicações do suporte a Unicode significam que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode armazenar dados em qualquer uma das linguagens com suporte pelo cliente e servidor de sistemas operacionais Windows, permissão de leitura, gravação, classificação e comparação de dados em qualquer conjunto de caracteres usado em um computador Windows. Aplicativos clientes de BI que consomem dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podem representar dados no idioma de preferência do usuário, supondo que os dados encontram-se no mesmo idioma do modelo.  
  
 Suporte a idiomas pode significar coisas diferentes para pessoas diferentes. A lista a seguir aborda algumas perguntas comuns relacionadas a como o Analysis Services dá suporte a idiomas.  
  
-   Dados, como já observado, são armazenados em qualquer conjunto de caracteres codificados com Unicode e encontrados no sistema operacional cliente Windows.  
  
-   Metadados, como nomes de objeto, podem ser traduzidos. Embora o suporte varie por tipo de modelo, modelos multidimensionais e de tabela dão suporte à adição de cadeias de caracteres traduzidas dentro do modelo. Você pode definir várias traduções e, em seguida, usar um identificador de localidade para determinar qual tradução é retornada ao cliente. Consulte [Recursos](#bkmk_features) abaixo para mais detalhes  
  
-   Erro, aviso e mensagens informativas retornadas pelo mecanismo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (msmdsrv) estão disponíveis em 43 idiomas com suporte pelo Office e Office 365. Nenhuma configuração é necessária para receber mensagens em um idioma específico. A localidade do aplicativo cliente determina quais cadeias de caracteres são retornadas.  
  
-   O arquivo de configuração (msmdsrv) e AMO PowerShell estão disponíveis apenas em inglês.  
  
-   Os arquivos de log conterão uma mistura mensagens em inglês e traduzidas, supondo que você instalou um pacote de idiomas no servidor Windows que executa o Analysis Services.  
  
-   Documentação e ferramentas, tais como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], são traduzidas para estes idiomas: Chinês simplificado, chinês tradicional, francês, alemão, italiano, japonês, coreano, português (Brasil), russo e espanhol. A cultura é especificada durante a instalação.  
  
 Para modelos multidimensionais, o Analysis Services permite a você definir idioma, ordenação e traduções de forma independente em toda a hierarquia de objetos.  Para modelos de tabela, você só pode adicionar traduções: ordenação e idioma são herdados pelo sistema operacional do host.  
  
 Os cenários habilitados por meio de recursos de globalização do Analysis Services incluem:  
  
-   Um modelo de dados fornece várias legendas traduzidas para que os valores e nomes de campos sejam exibidos no idioma de escolha do usuário. Para empresas que operam em países bilíngues como Suíça, Bélgica ou no Canadá, o suporte a vários idiomas em aplicativos cliente e servidor é um requisito padrão de codificação. Este cenário é habilitado por meio de traduções e conversões de moeda. Consulte [Recursos](#bkmk_features) abaixo para obter detalhes e links.  
  
-   Ambientes de desenvolvimento e produção estão localizados geograficamente em diferentes países. É cada vez mais comum desenvolver uma solução em um país e, em seguida, implantá-la em outro. Saber como definir as propriedades de ordenação e idioma é essencial se você ficar encarregado de preparar uma solução desenvolvida em um idioma para implantação em um servidor que usa um pacote de idiomas diferente. A configuração dessas propriedades permite substituir os padrões herdados que você obtém do sistema host original. Consulte [Idiomas e ordenações &amp;#40;Analysis Services&amp;#41;](../analysis-services/languages-and-collations-analysis-services.md) para obter detalhes sobre como definir propriedades.  
  
##  <a name="bkmk_features"></a> Recursos para compilar uma solução globalizada multilíngue  
 No nível do cliente, aplicativos globalizados que consomem ou manipulam dados multidimensionais do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podem usar os recursos multilíngues e multiculturais no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 É possível recuperar dados e metadados de objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nos quais foram definidas traduções automaticamente, fornecendo um identificador de localidade ao se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) para práticas de design e codificação que podem ajudá-lo a evitar problemas relacionados a dados em vários idiomas.  
  
||||  
|-|-|-|  
|**Recurso**|**Tabular**|**Multidimensional**|  
|[Idiomas e ordenações &amp;#40;Analysis Services&amp;#41;](../analysis-services/languages-and-collations-analysis-services.md)|Herdado do sistema operacional.|Herdado, mas com a capacidade de substituir o idioma e ordenação para os principais objetos na hierarquia de modelos.|  
|Escopo do suporte à tradução|Legendas e descrições.|Traduções podem ser criadas para nomes de objeto, legendas, identificadores e descrições, e também podem estar em qualquer script e linguagem Unicode. Isso é verdadeiro mesmo quando as ferramentas e o ambiente estão em outro idioma. Por exemplo, em um ambiente de desenvolvimento que usa o idioma inglês e uma ordenação latina em toda a pilha, você pode incluir em seu modelo de um objeto que usa caracteres cirílicos no nome.|  
|Implementando o suporte à tradução|Criar usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para gerar arquivos de tradução que você preenche e depois importa de volta para o modelo.<br /><br /> Consulte [Traduções em modelos de tabela &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md) para ver mais detalhes.|Crie usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir as traduções da legenda, descrição e tipos de conta para cubos e medidas, dimensão e atributos.<br /><br /> Consulte [Traduções em modelos multidimensionais &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md) para obter mais informações. Uma lição sobre como usar esse recurso pode ser encontrada em [lição 9: Definindo perspectivas e traduções](../analysis-services/lesson-9-defining-perspectives-and-translations.md) do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial.|  
|Conversão de moeda|Não disponível.|A conversão de moeda é por meio de scripts MDX especializados que convertem medidas contendo dados de moeda. Você pode usar o Assistente de Business Intelligence em [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] para gerar um script MDX que usa uma combinação de dados e metadados de dimensões, atributos e grupos de medidas para converter medidas contendo dados de moeda. Consulte [Conversões de moeda &#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a tradução no Analysis Services](../analysis-services/translation-support-in-analysis-services.md)   
 [Internacionalização para aplicativos do Windows](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Go Global Developer Center](http://msdn.microsoft.com/goglobal/bb871628.aspx)   
 [Gravando aplicativos da Windows Store com design adaptável baseado em localidade](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [Desenvolvendo aplicativos universais do Windows com C# e XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
