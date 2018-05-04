---
title: Noções básicas sobre o Analysis Services o Script de implantação | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35ebb4489ed72f370ffc4a2f2657f6caa5460714
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Compreendendo o script de implantação do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  O script de implantação XMLA gerado pelo Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consiste em duas seções:  
  
-   A primeira parte do script de implantação contém os comandos necessários para criar, alterar ou excluir os objetos adequados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados de destino. Por padrão, os arquivos de entrada gerados pelo projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são baseados em uma implantação incremental. Como resultado, o script de implantação XMLA afetará apenas os objetos que foram alterados ou excluídos.  
  
-   A segunda parte do script de implantação contém os comandos necessários para processar apenas os objetos criados ou alterados no servidor de destino (a opção Processar Padrão) ou processar o banco de dados de destino completamente. Você também pode escolher fazer com que o script de implantação não contenha nenhum comando de processamento.  
  
 O script de implantação inteiro pode ser executado em uma única transação ou em várias transações. Se o script for executado em várias transações, a primeira parte do script será executada como uma única transação e cada objeto será processado em sua própria transação.  
  
> [!IMPORTANT]  
>  O Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implanta apenas objetos em um único banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Não implanta nenhum objeto ou dados no nível do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Assistente de implantação do Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Noções básicas sobre os arquivos de entrada usados para criar o Script de implantação](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
