---
title: Implantar soluções modelo usando o Assistente de implantação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cde312f2bfad67c6cfe61a9b8379973c1f59a56c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026063"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Deploy Model Solutions Using the Deployment Wizard
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistente de implantação usa arquivos de saída do JSON gerados a partir de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto como arquivos de entrada. Esses arquivos de entrada são facilmente modificáveis para personalizar a implantação de um projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script de implantação gerado pode ser executado imediatamente ou pode ser salvo para implantação posterior.  

> [!NOTE]
> O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilitário da Assistente de implantação é instalado com o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Certifique-se de que você está usando a versão mais recente. Se executado no prompt de comando, por padrão, a versão mais recente do Assistente de implantação é instalada em C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio. 
  
 Você pode fazer a implantação usando o assistente conforme apresentado aqui. É possível automatizar a implantação ou usar o recurso Sincronizar. Se o banco de dados implantado for grande, considere o uso de partições em sistemas específicos. Você pode automatizar a população e a criação de partição usando o modelo de objeto de tabela (TOM), linguagem de Scriting de modelo de tabela (TMSL) e Analysis Management Objects (AMO).  
  
> [!IMPORTANT]  
>  Os arquivos de saída, nem o script de implantação conterá a id de usuário ou a senha se eles forem especificados em qualquer a cadeia de conexão para uma fonte de dados ou para fins de representação. Como eles são necessários para fins de processamento nesse cenário, você adicionará essas informações manualmente. Se a implantação não incluir processamento, você pode adicionar essa conexão e as informações de representação conforme necessário, depois da implantação. Se a implantação incluir processamento, você poderá adicionar essas informações dentro do assistente ou no script de implantação depois de ele ter sido salvo.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem como trabalhar com o Assistente para Implantação, com os arquivos de entrada e com o script de implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Executando o Assistente de implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Descreve os vários modos nos quais você pode executar o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|Descreve quais arquivos o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa como valores de entrada, o que cada um desses arquivos contém e fornece links para tópicos que descrevem como modificar os valores em cada um dos arquivos de entrada.|  
|[Noções básicas sobre o Script de implantação do Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Descreve o que o script de implantação contém e como o script é executado.|  
  
## <a name="see-also"></a>Consulte também  
 [Implantar soluções modelo usando XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [Implantar soluções modelo com o utilitário de implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
