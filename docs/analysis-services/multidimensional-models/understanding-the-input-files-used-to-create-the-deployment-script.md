---
title: "Compreendendo os arquivos de entrada usados para criar o script de implanta&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "arquivos de entrada [Analysis Services]"
  - "Assistente para Implantação do Analysis Services, scripts"
  - "implantando [Analysis Services], arquivos de entrada"
  - "Assistente para Implantação do Analysis Services, arquivos de entrada"
  - "scripts [Analysis Services], implantação"
  - "Implantações do Analysis Services, arquivos de entrada"
  - "modificando os arquivos de entrada"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Compreendendo os arquivos de entrada usados para criar o script de implanta&#231;&#227;o
  Quando você cria um projeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera arquivos XML para o projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca esses arquivos XML na pasta de saída do projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por padrão, a saída está fora na pasta \\Lixeira. A tabela a seguir lista os arquivos XML criados pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Arquivo XMLA|Description|  
|---------------|-----------------|  
|\<*nome do projeto*\>.asdatabase|Contém as definições declarativas para todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto.|  
|\<*nome do projeto*\>.deploymenttargets|Contém o nome da instância e do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão criados.|  
|\<*nome do projeto*\>.configsettings|Contém configurações específicas do ambiente, como informações de conexão de fonte de dados e locais de armazenamento de objeto. As configurações nesse arquivo substituem configurações no arquivo \<*nome do projeto*\>.asdatabase.|  
|\<*nome do projeto*\>.deploymentoptions|Contém opções de implantação como se a implantação é transacional e se objetos implantados deveriam ser processados depois da implantação.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca armazena senhas em seus arquivos de projeto.  
  
## Modificando os arquivos de entrada  
 Com a modificação dos valores nos arquivos de entrada ou dos valores recuperados nos arquivos de entrada, é possível alterar o destino de implantação, os parâmetros de configuração e opções de implantação sem editar todo o arquivo \<*nome do projeto*\>.asdatabase \(ou todo o arquivo de script XMLA se você gerar o script de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente\). A possibilidade de modificar arquivos individuais permite que você crie com facilidade scripts de implantação para diferentes finalidades.  
  
 Os tópicos seguintes explicam como modificar valores nos vários arquivos de entrada:  
  
-   [Especificando o destino de instalação](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [Especificando opções de processamento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## Consulte também  
 [Executando o Assistente para Implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Compreendendo o script de implantação do Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  