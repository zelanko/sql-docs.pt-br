---
title: "Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84106e3dcb54700770d8441d78634767feb5b9da
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Arquivos de Script de implantação - entrada usada para criar o Script de implantação
  Quando você cria um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera arquivos para o projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]coloca esses arquivos na pasta de saída do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. Por padrão, a saída está fora na pasta \Lixeira. A tabela a seguir lista os arquivos XML criados pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Arquivo|Description|  
|---------------|-----------------|  
|\<*nome do projeto*>. asdatabase|Um arquivo XMLA para projetos de modelo Tabular 1100/1103 ou Multidimensional, ou um arquivo JSON de tabela 1200 e maior projetos de modelo. Contém as definições declarativas para todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto.|  
|\<*nome do projeto*>. deploymenttargets|Contém o nome da instância e do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão criados.|  
|\<*nome do projeto*>. configsettings|Contém configurações específicas do ambiente, como informações de conexão de fonte de dados e locais de armazenamento de objeto. Configurações nesse arquivo substituem configurações no \< *nome do projeto*>. asdatabase.|  
|\<*nome do projeto*>. deploymentoptions|Contém opções de implantação como se a implantação é transacional e se objetos implantados deveriam ser processados depois da implantação.|  
  
> [!NOTE]  
>  O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca armazena senhas em seus arquivos de projeto.  
  
## <a name="modifying-the-input-files"></a>Modificando os arquivos de entrada  
 Modificar os valores nos arquivos de entrada, ou os valores recuperados dos arquivos de entrada, torna possível alterar o destino de implantação, as configurações e opções de implantação sem editar todo o \< *projeto nome*>. asdatabase (ou um arquivo de script inteiro se você gerar um script de um existente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados). A possibilidade de modificar arquivos individuais permite que você crie com facilidade scripts de implantação para diferentes finalidades.  
  
 Os tópicos seguintes explicam como modificar valores nos vários arquivos de entrada:  
  
-   [Especificando o destino de instalação](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificando opções de processamento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Assistente para Implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Noções básicas sobre o script de implantação do Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
