---
title: Reimplantação de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8b5ffb9f238fdc87ecb51765733f3a9cb632946
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005897"
---
# <a name="redeployment-of-packages"></a>Reimplantação de pacotes
  Após a implantação de um projeto, talvez seja necessário atualizar ou estender a funcionalidade de pacotes e reimplantar o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém os pacotes atualizados. Como parte do processo de reimplantação dos pacotes, você deve revisar as propriedades de configuração incluídas no utilitário de implantação. Por exemplo, você pode desejar não permitir mudanças de configuração depois que o pacote for reimplantado.  
  
## <a name="process-for-redeployment"></a>Processo de reimplantação  
 Após a conclusão da atualização dos pacotes, você deve recriar o projeto, copiar a pasta de implantação para o computador de destino e executar novamente o Assistente de Instalação de Pacotes.  
  
 Se você atualizar apenas alguns pacotes do projeto, talvez não queira reimplantar o projeto todo. Para implantar apenas alguns pacotes, você pode criar um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , adicionar os pacotes atualizados ao novo projeto e compilar e implantar o projeto. As configurações de pacotes são copiadas automaticamente com o pacote quando você adiciona o pacote a um projeto diferente.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implantar pacotes usando o utilitário de implantação](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  