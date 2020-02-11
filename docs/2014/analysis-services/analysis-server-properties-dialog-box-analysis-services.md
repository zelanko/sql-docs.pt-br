---
title: Caixa de diálogo Propriedades do Analysis Server (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b32b0fa678df98494f91c1026adebe701d807342
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062618"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>Caixa de diálogo Propriedades do Analysis Server (Analysis Services)
  Use a caixa de diálogo **Propriedades do Analysis Server** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir configurações gerais, de linguagem/agrupamento e segurança para uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Propriedades do Analysis Server** clicando com o botão direito do mouse em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Explorador de Objetos** e selecionando **Propriedades** no menu de contexto. A caixa de diálogo **Propriedades do Analysis Server** contém as propriedades a seguir.  
  
## <a name="information-properties"></a>Propriedades de informações  
 Use esta página para exibir o modo, a versão e o nível de compatibilidade do servidor. Cada instância é instalada no modo de servidor de Tabela ou Multidimensional, com a capacidade de carregar modelos de tabela ou multidimensionais. Se você precisar dar suporte aos dois modelos, instale duas instâncias.  
  
 O `DefaultCompatibilityLevel` **nível de compatibilidade com suporte** é equivalente à propriedade no amo. Ele é somente leitura, com base no modo de implantação de servidor especificado durante a instalação. O servidor verifica essa propriedade ao executar operações que variam por modo de servidor ou versão, como restaurar um backup de um banco de dados de tabela para uma instância de servidor de tabela. Não confunda isso com o modo de compatibilidade de banco de dados de modelos de tabela ou multidimensionais, que têm nomes e valores semelhantes. Os valores válidos para essa propriedade de servidor incluem:  
  
-   **1100** é o nível de compatibilidade padrão para um modo de implantação 0, para o modo multidimensional e Data Mining.  
  
-   **1103** é o nível de compatibilidade padrão para os modos de implantação 1 ou 2, para instalações que [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]dão suporte ao modo de tabela ou.  
  
 O servidor retorna esse valor quando um cliente que dá suporte ao namespace solicita DISCOVER_XML_METADATA. Consulte [Conjunto de linhas DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset) para obter mais detalhes.  
  
## <a name="general-properties"></a>Propriedades gerais  
 Use essa página para definir as propriedades gerais básicas e avançadas, como configurações de locais de pasta e de rede, para uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 A página de propriedades do servidor mostra apenas as propriedades com maior probabilidade de alteração por um administrador, como memória e propriedades de pool de threads usadas para ajustar o servidor para determinadas configurações. A seguinte lista fornece links para os principais grupos de propriedades:  
  
-   [Propriedades gerais](server-properties/general-properties.md)  
  
-   [Propriedades de mineração de dados](server-properties/data-mining-properties.md)  
  
-   [Propriedades de recurso](server-properties/feature-properties.md)  
  
-   [Propriedades FileStore](server-properties/filestore-properties.md)  
  
-   [Propriedades do gerenciador de bloqueio](server-properties/lock-manager-properties.md)  
  
-   [Propriedades do log](server-properties/log-properties.md)  
  
-   [Propriedades de memória](server-properties/memory-properties.md)  
  
-   [Propriedades de rede](server-properties/network-properties.md)  
  
-   [Propriedades OLAP](server-properties/olap-properties.md)  
  
-   [Propriedades de segurança](server-properties/security-properties.md)  
  
-   [Propriedades de pool de threads](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>Propriedades de Idioma/Ordenação  
 Use essa página para definir opções de ordenação e idioma padrão para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A lista a seguir contém breves descrições de cada opção. Consulte [Idiomas e ordenações &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md) para obter detalhes.  
  
-   **Binary** é usado para classificar e comparar dados com base nos padrões de bits definidos para cada caractere. A ordem de classificação binária diferencia maiúsculas e minúsculas, isto é, minúscula precede maiúscula, e diferencia acento. Essa é a ordem de classificação mais rápida.  
  
     Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seguirá as regras de classificação e comparação definidas em dicionários do idioma ou alfabeto associado.  
  
    > [!NOTE]  
    >  Se esta opção estiver selecionada, as opções **Diferenciar Maiúsculas de Minúsculas**, **Diferenciar Acento**, **Distinguir Caracteres Kana**e **Distinguir Largura** estarão desabilitadas.  
  
-   **Binary 2** é usado para classificar e comparar dados Unicode com base nos padrões de bit definidos para cada caractere. A ordem de classificação binária diferencia maiúsculas e minúsculas, isto é, minúscula precede maiúscula, e diferencia acento. Essa é a ordem de classificação mais rápida.  
  
-   Diferenciar **maiúsculas de minúsculas** é usado para classificar e comparar dados com base nas regras de dicionário fornecidas para o idioma ou alfabeto associado e para distinguir entre letras maiúsculas e minúsculas.  
  
     Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que as versões maiúsculas e minúsculas de letras são iguais. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]não define se letras minúsculas devem ser classificadas em uma posição inferior ou superior em relação a letras maiúsculas quando **a diferenciação de maiúsculas** e minúsculas não está selecionada.  
  
-   **Diferenciar acento** é usado para classificar e comparar dados com base nas regras de dicionário fornecidas para o idioma ou alfabeto associado e para distinguir entre caracteres acentuados e não acentuados. Por exemplo, 'a' não é igual a 'á'.  
  
     Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que as versões acentuadas e não acentuadas de letras são iguais.  
  
-   **Diferenciar Kana** é usado para e comparar dados com base nas regras de dicionário fornecidas para o idioma ou alfabeto associado e para distinguir entre os dois tipos de caracteres kana japoneses: hiragana e Katakana.  
  
     Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que caracteres Hiragana e Katakana são iguais.  
  
-   A **diferenciação de largura** é usada para classificar e comparar dados com base nas regras de dicionário fornecidas para o idioma ou alfabeto associado e para distinguir entre um caractere de byte único (meia largura) e o mesmo caractere quando representado como um caractere de byte duplo (largura inteira).  
  
     Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará as representações de byte único e de byte duplo do mesmo caractere como iguais.  
  
## <a name="security-properties"></a>Propriedades de segurança  
 Use essa página para especificar as contas de usuário e grupo do Windows pertencentes à função de administrador do servidor para uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . A associação nessa função transmite a permissão para executar tarefas em todo o servidor, como criar ou processar um banco de dados, modificar propriedades do servidor, adicionar/remover outros membros dessa função ou iniciar um rastreamento. Consulte [conceder permissões de administrador do servidor &#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para obter detalhes.  
  
## <a name="see-also"></a>Consulte Também  
 [Determinar o modo de servidor de uma instância de Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Configurar propriedades do servidor no Analysis Services](server-properties/server-properties-in-analysis-services.md)   
 [Metodologias de autenticação com suporte pelo Analysis Services](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Funções e permissões &#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Linguagens e agrupamentos &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
