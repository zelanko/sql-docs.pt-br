---
title: "Especificando op&#231;&#245;es de implanta&#231;&#227;o de fun&#231;&#227;o e de parti&#231;&#227;o | Microsoft Docs"
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
  - "partições [Analysis Services], opções de implantação"
  - "implantações do Analysis Services, funções"
  - "implantações do Analysis Services, partições"
  - "Assistente para Implantação do Analysis Services, funções"
  - "Assistente para Implantação do Analysis Services, partições"
  - "implantação [Analysis Services], funções"
  - "funções [Analysis Services], opções de implantação"
  - "implantação [Analysis Services], partições"
  - "modificando implantações de função"
  - "modificando implantações de partição"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Especificando op&#231;&#245;es de implanta&#231;&#227;o de fun&#231;&#227;o e de parti&#231;&#227;o
  O Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lê as opções de partição e de implantação de função do arquivo \<*nome do projeto*>.deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa as opções de implantação de partição e de função do projeto atual quando o arquivo \<*nome do projeto*>.deploymentoptions é criado. Para obter mais informações sobre parâmetros de configuração, consulte [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md).  
  
## Revisando as opções de implantação de partição e de função  
 As opções de implantação no arquivo \<*nome do projeto*>.deploymentoptions incluem o seguinte:  
  
 **Opções de implantação de partição**  
 O arquivo \<*nome do projeto*>.deploymentoptions especifica se as partições existentes no banco de dados de destino são retidas ou sobrescritas (padrão). Se as partições existentes forem retidas, só serão implantadas partições novas e os projetos de partições e agregação em todos os grupos de medidas existentes ficarão inalterados.  
  
> [!NOTE]  
>  Se o grupo de medidas no qual a partição existe for excluído, a partição será excluída automaticamente.  
  
 **Opções de implantação de função**  
 O arquivo \<*nome do projeto*>.deploymentoptions especifica as seguintes opções de implantação de função:  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e apenas novas funções e membros de função são implantados.  
  
-   Todas as funções e os membros de função existentes no banco de dados de destino são substituídos pelas funções e pelos membros sendo implantados.  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e nenhuma nova função será implantada.  
  
-   **Nota** Quando funções e membros existentes são retidos, as permissões associadas a essas funções são redefinidas como nenhuma. As permissões de segurança são contidas pelos objetos que protegem, não pelas funções de segurança com que estão associadas. Para obter mais informações sobre como trabalhar com esse comportamento usando o Assistente para Implantação do Analysis Service, consulte “Retenção de funções e membros” na Base de Dados de Conhecimento Microsoft.  
  
## Modificando as opções de implantação de partição e de função  
 Pode ser necessário implantar o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando opções de partição e de função diferentes das armazenadas no arquivo \<*nome do projeto*>.deploymentoptions. Por exemplo, pode ser necessário reter partições, funções e membros de função existentes, em vez de substituir todas as partições, funções e membros existentes, conforme indicado no arquivo \<*nome do projeto*>.deploymentoptions.  
  
 Para modificar a implantação de partições e funções em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você não pode mudar as definições de partição e de funções dentro do projeto porque a caixa de diálogo *\<nome do projeto>* **Páginas de Propriedade** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não exibe essas opções. Se você quiser mudar as opções de implantação para funções e partições, será necessário alterar essas informações dentro do próprio arquivo \<*nome do projeto*>.deploymentoptions. O procedimento a seguir descreve como alterar as opções de implantação de partição e de função dentro do arquivo \<*nome do projeto*>.deploymentoptions.  
  
#### Para alterar a implantação de partições ou de funções depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interativamente, e na página **Opções de implantação de partição e de função** , especifique as novas opções de implantação para as partições e funções.  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para ser executado em modo de arquivo de resposta. (Para obter mais informações sobre o modo de arquivo de resposta, consulte [Executando o Assistente de Implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).)  
  
     — ou —  
  
-   Abra o arquivo \<*nome do projeto*>.deploymentoptions em qualquer editor de texto e mude manualmente as opções.  
  
## Consulte também  
 [Especificando o destino de instalação](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Especificando opções de processamento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  