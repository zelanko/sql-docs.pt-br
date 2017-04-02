---
title: "Especificando o destino de instala&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "arquivos de entrada [Analysis Services]"
  - "destinos de instalação [Analysis Services]"
  - "implantações do Analysis Services, destinos de instalação"
  - "Assistente de Implantação do Analysis Services, destinos de instalação"
  - "implantando [Analysis Services], destinos de instalação"
  - "modificando destinos de instalação"
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Especificando o destino de instala&#231;&#227;o
  O Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lê as informações sobre o destino da instalação no arquivo \<*nome do projeto*>.deploymenttargets. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa o banco de dados e o servidor especificados na página **Implantação** da caixa de diálogo *\<nome do projeto>* **Páginas de Propriedades** para criar o arquivo \<*nome do projeto*>.targets.  
  
## Modificando o destino de instalação para a implantação  
 Em alguns casos, talvez seja necessário implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um banco de dados ou instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente do especificado na página **Implantação**. Por exemplo, você talvez queira implantar o projeto em um servidor para teste antes da implantação e, em seguida, implantá-lo em um servidor de produção após a conclusão do teste. Também é possível implantar um projeto concluído e testado em vários servidores de produção em um cluster de Balanceamento de Carga de Rede ou em um servidor de preparação e em um de produção.  
  
 Para implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um banco de dados ou instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente, altere o destino de instalação no arquivo de entrada usando um dos métodos descritos no procedimento a seguir.  
  
#### Para alterar o destino de instalação depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de modo interativo. Na página **Destino da Instalação**, especifique um novo destino para a instância e o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     — ou —  
  
-   Modifique o arquivo \<*nome do projeto*>.deploymenttargets usando qualquer editor de texto.  
  
## Consulte também  
 [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Especificando opções de processamento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  