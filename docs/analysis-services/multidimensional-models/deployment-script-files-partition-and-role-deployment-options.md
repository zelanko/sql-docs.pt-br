---
title: "Especificando opções de implantação de função e partição | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2c23117a8f5765855988480c6b018fd84e1ee0de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>Arquivos de Script de implantação - partição e opções de implantação de função
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação do lê as opções de implantação de partição e de função do \< *nome do projeto*>. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa as opções de implantação de partição e de função do atual projeto quando o \< *nome do projeto*>. deploymentoptions é criado. Para obter mais informações sobre parâmetros de configuração, consulte [Compreendendo os arquivos de entrada usados para criar o script de implantação](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Revisando as opções de implantação de partição e de função  
 As opções de implantação no \< *nome do projeto*>. deploymentoptions incluem o seguinte:  
  
 **Opções de implantação de partição**  
 O \< *nome do projeto*>. deploymentoptions Especifica se as partições existentes no banco de dados de destino são retidas ou sobrescritas (padrão). Se as partições existentes forem retidas, só serão implantadas partições novas e os projetos de partições e agregação em todos os grupos de medidas existentes ficarão inalterados.  
  
> [!NOTE]  
>  Se o grupo de medidas no qual a partição existe for excluído, a partição será excluída automaticamente.  
  
 **Opções de implantação de função**  
 O \< *nome do projeto*>. deploymentoptions Especifica uma das seguintes opções de implantação de função:  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e apenas novas funções e membros de função são implantados.  
  
-   Todas as funções e os membros de função existentes no banco de dados de destino são substituídos pelas funções e pelos membros sendo implantados.  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e nenhuma nova função será implantada.  
  
-   **Nota** Quando funções e membros existentes são retidos, as permissões associadas a essas funções são redefinidas como nenhuma. As permissões de segurança são contidas pelos objetos que protegem, não pelas funções de segurança com que estão associadas. Para obter mais informações sobre como trabalhar com esse comportamento usando o Assistente para Implantação do Analysis Service, consulte “Retenção de funções e membros” na Base de Dados de Conhecimento Microsoft.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modificando as opções de implantação de partição e de função  
 Talvez seja necessário implantar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto usando opções de partição e de função diferentes das armazenadas no \< *nome do projeto*>. deploymentoptions. Por exemplo, você poderá desejar reter partições existentes, funções e membros da função, em vez de substituir todas as partições existentes, funções e membros conforme indicado no \< *nome do projeto*>. deploymentoptions.  
  
 Para modificar a implantação de partições e funções em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto, você não pode alterar as configurações de partição e de funções dentro do projeto porque o  *\<nome do projeto >* **páginas de propriedades**  da caixa de diálogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não exibe essas opções. Se você quiser alterar as opções de implantação para funções e partições, você deve alterar essas informações dentro de \< *nome do projeto*>. deploymentoptions em si. O procedimento a seguir descreve como alterar as opções de implantação de partição e de função dentro de \< *nome do projeto*>. deploymentoptions.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Para alterar a implantação de partições ou de funções depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interativamente, e na página **Opções de implantação de partição e de função** , especifique as novas opções de implantação para as partições e funções.  
  
     — ou —  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para ser executado em modo de arquivo de resposta. (Para obter mais informações sobre o modo de arquivo de resposta, consulte [Executando o Assistente de Implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).)  
  
     — ou —  
  
-   Abra o \< *nome do projeto*>. deploymentoptions em qualquer editor de texto e manualmente alterar as opções.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando o destino de instalação](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Especificando opções de processamento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
