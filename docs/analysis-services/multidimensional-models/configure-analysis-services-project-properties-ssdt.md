---
title: Configurar propriedades de projeto do Analysis Services (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90fd3a238d7b4ab3e573c4ecef76bdbdd3bde7f1
ms.sourcegitcommit: 3f19c843b38d3835d07921612f0143620eb9a0e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53709799"
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Configurar propriedades do projeto do Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é definido com certas propriedades padrão que afetam a construção e a implantação do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para alterar as propriedades do projeto, clique com o botão direito do mouse no objeto de projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e em **Propriedades**. Alternativamente, você pode clicar em **Propriedades** no menu de Projeto.  
  
## <a name="property-description"></a>Descrição da Propriedade  
 A tabela a seguir descreve cada propriedade do projeto, lista seu valor padrão e fornece informações sobre como alterar seu valor.  
  
|Propriedade|Configuração padrão|Descrição|  
|--------------|---------------------|-----------------|  
|Construir / Deployment Server Edition|A edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para desenvolver o projeto.|Especifica a edição do servidor no qual os projetos serão finalmente implantados. Quando houver vários desenvolvedores trabalhando em um projeto, eles precisam entender a edição do servidor para saber quais recursos incorporar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Build / versão do servidor de implantação|A versão usada para desenvolver os projetos.|Especifica a versão do servidor no qual os projetos serão finalmente implantados.|  
|Construir / Saídas|/bin|O caminho relativo para a saída do processo de construção do projeto.|  
|Construir / Remover Senhas|True|Especifica se as senhas conhecidas serão removidas das cadeias de conexão que são gravadas no diretório de saída do processo de construção. As senhas são removidas para aumentar a segurança. Se as senhas forem removidas, será necessário fornecê-las quando o projeto implantado for processado para que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] acesse a fonte de dados.|  
|Depuração / Objeto Inicial|\<Objeto atualmente ativo >|Determina o objeto que será iniciado quando você começar a depuração.|  
|Implantação / Modo de Implantação|Implantar Apenas Alterações|Por padrão, apenas as alterações feitas nos objetos do projeto são implantadas (desde que nenhuma outra alteração tenha sido feita nos objetos diretamente de fora do projeto). Você também pode optar pela implantação de todos os objetos durante cada implantação. Para um melhor desempenho, use Implantar Apenas Alterações.|  
|Implantação / Opção de Processamento|Padrão|Por padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determinará o tipo de processamento exigido quando as alterações a objetos forem implantadas. Geralmente, resulta em tempo menor de implantação. No entanto, você também pode optar pelo processamento completo ou por não fazer o processamento a cada implantação.|  
|Implantação / Implantação Transacional|Falso|Por padrão, a implantação de objetos alterados ou de todos eles não é transacional com o processamento desses objetos implantados. A implantação pode ser bem-sucedida e persistir mesmo em caso de falha do processamento. Você pode alterar esse padrão para incorporar a implantação e o processando em uma única transação.|  
|Servidor de implantação / destino|localhost|Por padrão, os objetos de banco de dados do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão implantados na instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no computador local no qual o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] está sendo usado. Altere esse padrão para especificar uma instância nomeada no computador local ou uma instância em algum outro computador remoto no qual você tenha permissão para criar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Implantação / Banco de dados|\<nome do projeto >|Por padrão, o nome do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no qual os objetos do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão instanciados após a implantação é o nome do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no momento em que foi definido. Altere essa propriedade para mudar o nome do banco de dados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada pela propriedade Servidor.|  
  
## <a name="property-configurations"></a>Configurações de Pacote  
 As propriedades são definidas por configuração. As configurações do projeto permitem que os desenvolvedores trabalhem em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com configurações diferentes de construção, depuração e implantação sem editar diretamente os arquivos de projeto XML subjacentes.  
  
 Um projeto é criado inicialmente com uma única configuração, chamada Desenvolvimento. Você pode criar configurações adicionais e alternar entre as configurações usando o Gerenciador de Configurações.  
  
 Enquanto não são criadas configurações adicionais, todos os desenvolvedores usam essa configuração comum. No entanto, durante as várias fases de desenvolvimento - do projeto, como durante o desenvolvimento inicial e teste de um projeto - diferentes desenvolvedores será podem usar diferentes fontes de dados e implantar o projeto em servidores diferentes para diferentes finalidades. Com as configurações, é possível manter esses parâmetros distintos em arquivos de configuração diferentes.  
  
## <a name="see-also"></a>Consulte também  
 [Criar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
