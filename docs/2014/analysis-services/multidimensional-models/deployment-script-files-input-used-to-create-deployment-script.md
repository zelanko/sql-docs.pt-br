---
title: Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 396d52a32e7ead5b625534e3ce4c60fafbddc6aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117762"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>Compreendendo os arquivos de entrada usados para criar o script de implantação
  Quando você cria um projeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gera arquivos XML para o projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca esses arquivos XML na pasta de saída do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. Por padrão, a saída está fora na pasta \Lixeira. A tabela a seguir lista os arquivos XML criados pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Arquivo XMLA|Description|  
|---------------|-----------------|  
|\<*nome do projeto*>. asdatabase|Contém as definições declarativas para todos os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no projeto.|  
|\<*nome do projeto*>. deploymenttargets|Contém o nome da instância e do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que os objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão criados.|  
|\<*nome do projeto*>. configsettings|Contém configurações específicas do ambiente, como informações de conexão de fonte de dados e locais de armazenamento de objeto. Configurações nesse arquivo substituem configurações no \< *nome do projeto*>. asdatabase.|  
|\<*nome do projeto*>. deploymentoptions|Contém opções de implantação como se a implantação é transacional e se objetos implantados deveriam ser processados depois da implantação.|  
  
> [!NOTE]  
>  O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca armazena senhas em seus arquivos de projeto.  
  
## <a name="modifying-the-input-files"></a>Modificando os arquivos de entrada  
 Modificar os valores nos arquivos de entrada, ou os valores recuperados dos arquivos de entrada, torna possível alterar o destino de implantação, as configurações e opções de implantação sem editar todo o \< *projeto nome*>. asdatabase (ou um arquivo de script XMLA inteiro se você gerar um script de um existente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados). A possibilidade de modificar arquivos individuais permite que você crie com facilidade scripts de implantação para diferentes finalidades.  
  
 Os tópicos seguintes explicam como modificar valores nos vários arquivos de entrada:  
  
-   [Especificando o destino de instalação](deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificando opções de implantação de função e de partição](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificando opções de processamento](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Assistente de implantação do Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Noções básicas sobre o script de implantação do Analysis Services](understanding-the-analysis-services-deployment-script.md)  
  
  