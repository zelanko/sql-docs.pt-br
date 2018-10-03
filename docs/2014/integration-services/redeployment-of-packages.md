---
title: Reimplantação de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2612fa2930147c5a655ec13bd3adbdf3c4bd7cd0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195584"
---
# <a name="redeployment-of-packages"></a>Reimplantação de pacotes
  Após a implantação de um projeto, talvez seja necessário atualizar ou estender a funcionalidade de pacotes e reimplantar o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém os pacotes atualizados. Como parte do processo de reimplantação dos pacotes, você deve revisar as propriedades de configuração incluídas no utilitário de implantação. Por exemplo, você pode desejar não permitir mudanças de configuração depois que o pacote for reimplantado.  
  
## <a name="process-for-redeployment"></a>Processo de reimplantação  
 Após a conclusão da atualização dos pacotes, você deve recriar o projeto, copiar a pasta de implantação para o computador de destino e executar novamente o Assistente de Instalação de Pacotes.  
  
 Se você atualizar apenas alguns pacotes do projeto, talvez não queira reimplantar o projeto todo. Para implantar apenas alguns pacotes, você pode criar um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , adicionar os pacotes atualizados ao novo projeto e compilar e implantar o projeto. As configurações de pacotes são copiadas automaticamente com o pacote quando você adiciona o pacote a um projeto diferente.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implantar pacotes usando o utilitário de implantação](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
