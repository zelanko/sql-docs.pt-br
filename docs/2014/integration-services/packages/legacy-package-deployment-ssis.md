---
title: Pacote de implantação (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7a732d2b3c8371d0bb5637cbe19101640e8d81a1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020044"
---
# <a name="package-deployment-ssis"></a>Implantação de pacotes (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui ferramentas e assistentes que simplificam a implantação de pacotes do computador de desenvolvimento para o servidor de produção ou para outros computadores.  
  
 Há quatro etapas no processo de implantação de pacotes:  
  
1.  A primeira etapa é opcional e envolve a criação de configurações de pacotes que atualizam as propriedades dos elementos dos pacotes em tempo de execução. As configurações são incluídas automaticamente quando se implantam os pacotes.  
  
2.  A segunda etapa é desenvolver o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para criar um utilitário de implantação de pacote. O utilitário de implantação para o projeto contém os pacotes que você quer implantar  
  
3.  A terceira etapa é copiar a pasta de implantação que foi criada quando você desenvolveu o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o computador de destino.  
  
4.  A quarta etapa é executar no computador de destino o Assistente de Instalação de Pacotes para instalar os pacotes no sistema de arquivos ou em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como criar um utilitário de implantação, consulte [Criar um utilitário de implantação](../create-a-deployment-utility.md).  
  
 Para obter informações sobre como implantar pacotes usando o utilitário de implantação, consulte [Implantar pacotes usando o utilitário de implantação](../deploy-packages-by-using-the-deployment-utility.md).  
  
 Para obter informações sobre como criar configurações de pacote, consulte [Criar configurações de pacote](../create-package-configurations.md).  
  
  