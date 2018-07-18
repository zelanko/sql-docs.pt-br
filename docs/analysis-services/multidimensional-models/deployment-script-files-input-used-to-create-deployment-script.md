---
title: Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b75ec5d7433931a81a0fa6e2c648f85335fbedc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002188"
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Arquivos de Script de implantação – entrada usada para criar Script de implantação
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Quando você cria um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera arquivos para o projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca esses arquivos na pasta de saída de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. Por padrão, a saída está fora na pasta \Lixeira. A tabela a seguir lista os arquivos XML criados pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Arquivo|Description|  
|---------------|-----------------|  
|\<*nome do projeto*>. asdatabase|Um arquivo XMLA para Multidimensional ou projetos de modelo Tabular 1100/1103 ou um arquivo JSON para Tabular 1200 e maior projetos de modelo. Contém as definições declarativas para todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto.|  
|\<*nome do projeto*>. deploymenttargets|Contém o nome da instância e do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão criados.|  
|\<*nome do projeto*>. configsettings|Contém configurações específicas do ambiente, como informações de conexão de fonte de dados e locais de armazenamento de objeto. Configurações nesse arquivo substituem configurações na \< *nome do projeto*>. asdatabase.|  
|\<*nome do projeto*>. deploymentoptions|Contém opções de implantação como se a implantação é transacional e se objetos implantados deveriam ser processados depois da implantação.|  
  
> [!NOTE]  
>  O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca armazena senhas em seus arquivos de projeto.  
  
## <a name="modifying-the-input-files"></a>Modificando os arquivos de entrada  
 Modificar os valores nos arquivos de entrada, ou os valores recuperados dos arquivos de entrada, torna possível alterar o destino de implantação, os parâmetros de configuração e opções de implantação sem editar todo o \< *projeto nome da*>. asdatabase (ou um arquivo de script inteiro se você gerar um script de uma já existente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados). A possibilidade de modificar arquivos individuais permite que você crie com facilidade scripts de implantação para diferentes finalidades.  
  
 Os tópicos seguintes explicam como modificar valores nos vários arquivos de entrada:  
  
-   [Especificando o destino de instalação](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificando opções de implantação de função e de partição](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificando definições de configuração para implantação de solução](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificando opções de processamento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Assistente para Implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Noções básicas sobre o script de implantação do Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
