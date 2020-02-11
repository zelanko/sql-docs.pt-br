---
title: Noções básicas sobre os arquivos de entrada usados para criar o script de implantação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dec93494dd21412c067af293832066087ca3ed37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075409"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>Compreendendo os arquivos de entrada usados para criar o script de implantação
  Quando você cria um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , o gera arquivos XML para o projeto. O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca esses arquivos XML na pasta de saída do projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por padrão, a saída está fora na pasta \Lixeira. A tabela a seguir lista os arquivos XML criados pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Arquivo XMLA|DESCRIÇÃO|  
|---------------|-----------------|  
|\<*nome do projeto*>. asdatabase|Contém as definições declarativas para todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto.|  
|\<*nome do projeto*>. deploymenttargets|Contém o nome da instância e do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão criados.|  
|\<*nome do projeto*>. configsettings|Contém configurações específicas do ambiente, como informações de conexão de fonte de dados e locais de armazenamento de objeto. As configurações nesse arquivo substituem as configurações \<no arquivo *nome do projeto*>. asdatabase.|  
|\<*nome do projeto*>. deploymentoptions|Contém opções de implantação como se a implantação é transacional e se objetos implantados deveriam ser processados depois da implantação.|  
  
> [!NOTE]  
>  
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca armazena senhas em seus arquivos de projeto.  
  
## <a name="modifying-the-input-files"></a>Modificando os arquivos de entrada  
 Modificar os valores nos arquivos de entrada ou os valores recuperados dos arquivos de entrada torna possível alterar o destino da implantação, as definições de configuração e as opções de implantação sem editar todo \<o nome do *projeto*> arquivo. asdatabase (ou um arquivo de script XMLA inteiro se você gerar um script a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] partir de um banco de dados existente). A possibilidade de modificar arquivos individuais permite que você crie com facilidade scripts de implantação para diferentes finalidades.  
  
 Os tópicos seguintes explicam como modificar valores nos vários arquivos de entrada:  
  
-   [Especificando o destino de instalação](deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificando opções de implantação de função e de partição](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificando opções de processamento](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Executando o assistente de implantação do Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Compreendendo o script de implantação do Analysis Services](understanding-the-analysis-services-deployment-script.md)  
  
  
