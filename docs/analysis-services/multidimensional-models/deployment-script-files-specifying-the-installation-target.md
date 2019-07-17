---
title: Especificando o destino de instalação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c9b5e72bdf58cf10f3ab30db720a2434ff9e41b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208936"
---
# <a name="deployment-script-files---specifying-the-installation-target"></a>Arquivos de Script de implantação – especificar o destino de instalação
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação do lê as informações de destino da instalação dos \< *nome do projeto*>. deploymenttargets arquivo. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria esse arquivo quando você cria o projeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa o banco de dados e servidor especificados na **implantação** página do  *\<nome do projeto >* **páginas de propriedades** caixa de diálogo para criar o \< *nome do projeto*> arquivo. targets.  
  
## <a name="modifying-the-installation-target-for-deployment"></a>Modificando o destino de instalação para a implantação  
 Em alguns casos, talvez seja necessário implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um banco de dados ou instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente do especificado na página **Implantação** . Por exemplo, você talvez queira implantar o projeto em um servidor para teste antes da implantação e, em seguida, implantá-lo em um servidor de produção após a conclusão do teste. Também é possível implantar um projeto concluído e testado em vários servidores de produção em um cluster de Balanceamento de Carga de Rede ou em um servidor de preparação e em um de produção.  
  
 Para implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um banco de dados ou instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferente, altere o destino de instalação no arquivo de entrada usando um dos métodos descritos no procedimento a seguir.  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>Para alterar o destino de instalação depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de modo interativo. Na página **Destino da Instalação** , especifique um novo destino para a instância e o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     - ou -  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para executar em modo de arquivo de resposta. Para obter mais informações sobre o modo de arquivo de resposta, consulte [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     - ou -  
  
-   Modificar a \< *nome do projeto*> arquivo. deploymenttargets usando qualquer editor de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Especificando opções de processamento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
