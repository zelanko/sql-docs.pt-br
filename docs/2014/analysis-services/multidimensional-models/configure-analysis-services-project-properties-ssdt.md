---
title: Configurar propriedades do projeto Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.BUSINESS_INTELLIGENCE_DESIGNERS.ANALYSIS_SERVICES_DESIGNERS.GENERAL
helpviewer_keywords:
- projects [Analysis Services], properties
ms.assetid: d9786c66-7d8c-48e3-950d-3f25044b4ce2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 85f67836e2d7dcb7ea17244398867ce5c3cc3364
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537038"
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Configurar propriedades do projeto do Analysis Services (SSDT)
  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é definido com certas propriedades padrão que afetam a construção e a implantação do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para alterar as propriedades do projeto, clique com o botão direito do mouse no objeto de projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e em **Propriedades**. Alternativamente, você pode clicar em **Propriedades** no menu de Projeto.  
  
## <a name="property-description"></a>Descrição da Propriedade  
 A tabela a seguir descreve cada propriedade do projeto, lista seu valor padrão e fornece informações sobre como alterar seu valor.  
  
|Propriedade|Configuração padrão|Description|  
|--------------|---------------------|-----------------|  
|Construir / Deployment Server Edition|A edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para desenvolver o projeto.|Especifica a edição do servidor no qual os projetos serão finalmente implantados. Quando houver vários desenvolvedores trabalhando em um projeto, eles precisam entender a edição do servidor para saber quais recursos incorporar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Construir / Deployment Server Edition|A versão usada para desenvolver os projetos.|Especifica a versão do servidor no qual os projetos serão finalmente implantados.|  
|Construir / Saídas|/bin|O caminho relativo para a saída do processo de construção do projeto.|  
|Construir / Remover Senhas|True|Especifica se as senhas conhecidas serão removidas das cadeias de conexão que são gravadas no diretório de saída do processo de construção. As senhas são removidas para aumentar a segurança. Se as senhas forem removidas, será necessário fornecê-las quando o projeto implantado for processado para que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] acesse a fonte de dados.|  
|Depuração / Objeto Inicial|\<Currently Active Object>|Determina o objeto que será iniciado quando você começar a depuração.|  
|Implantação / Modo de Implantação|Implantar Apenas Alterações|Por padrão, apenas as alterações feitas nos objetos do projeto são implantadas (desde que nenhuma outra alteração tenha sido feita nos objetos diretamente de fora do projeto). Você também pode optar pela implantação de todos os objetos durante cada implantação. Para um melhor desempenho, use Implantar Apenas Alterações.|  
|Implantação / Opção de Processamento|Padrão|Por padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determinará o tipo de processamento exigido quando as alterações a objetos forem implantadas. Geralmente, resulta em tempo menor de implantação. No entanto, você também pode optar pelo processamento completo ou por não fazer o processamento a cada implantação.|  
|Implantação / Implantação Transacional|Falso|Por padrão, a implantação de objetos alterados ou de todos eles não é transacional com o processamento desses objetos implantados. A implantação pode ser bem-sucedida e persistir mesmo em caso de falha do processamento. Você pode alterar esse padrão para incorporar a implantação e o processando em uma única transação.|  
|Servidor de implantação / destino|localhost|Por padrão, os objetos de banco de dados do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão implantados na instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no computador local no qual o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] está sendo usado. Altere esse padrão para especificar uma instância nomeada no computador local ou uma instância em algum outro computador remoto no qual você tenha permissão para criar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Implantação / Banco de dados|\<project name>|Por padrão, o nome do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no qual os objetos do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão instanciados após a implantação é o nome do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no momento em que foi definido. Altere essa propriedade para mudar o nome do banco de dados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada pela propriedade Servidor.|  
  
## <a name="property-configurations"></a>Configurações de Pacote  
 As propriedades são definidas por configuração. As configurações do projeto permitem que os desenvolvedores trabalhem em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com configurações diferentes de construção, depuração e implantação sem editar diretamente os arquivos de projeto XML subjacentes.  
  
 Um projeto é criado inicialmente com uma única configuração, chamada Desenvolvimento. Você pode criar configurações adicionais e alternar entre as configurações usando o Gerenciador de Configurações.  
  
 Enquanto não são criadas configurações adicionais, todos os desenvolvedores usam essa configuração comum. No entanto, durante as várias fases do desenvolvimento de projetos, como durante o desenvolvimento inicial e o teste de um projeto, diferentes desenvolvedores poderão usar fontes de dados diferentes e implantar o projeto em servidores diferentes para diferentes finalidades. Com as configurações, é possível manter esses parâmetros distintos em arquivos de configuração diferentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Compilar projetos de Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
