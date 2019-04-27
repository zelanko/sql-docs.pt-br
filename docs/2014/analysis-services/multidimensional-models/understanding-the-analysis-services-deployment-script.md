---
title: Noções básicas sobre a análise de serviços de Script de implantação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84bc0e699a0fb47b78b1b0d075a0ef87c8a4dcc3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741106"
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Compreendendo o script de implantação do Analysis Services
  O script de implantação XMLA gerado pelo Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consiste em duas seções:  
  
-   A primeira parte do script de implantação contém os comandos necessários para criar, alterar ou excluir os objetos adequados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados de destino. Por padrão, os arquivos de entrada gerados pelo projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são baseados em uma implantação incremental. Como resultado, o script de implantação XMLA afetará apenas os objetos que foram alterados ou excluídos.  
  
-   A segunda parte do script de implantação contém os comandos necessários para processar apenas os objetos criados ou alterados no servidor de destino (a opção Processar Padrão) ou processar o banco de dados de destino completamente. Você também pode escolher fazer com que o script de implantação não contenha nenhum comando de processamento.  
  
 O script de implantação inteiro pode ser executado em uma única transação ou em várias transações. Se o script for executado em várias transações, a primeira parte do script será executada como uma única transação e cada objeto será processado em sua própria transação.  
  
> [!IMPORTANT]  
>  O Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implanta apenas objetos em um único banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Não implanta nenhum objeto ou dados no nível do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Assistente para Implantação do Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Compreendendo os arquivos de entrada usados para criar o script de implantação](deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
