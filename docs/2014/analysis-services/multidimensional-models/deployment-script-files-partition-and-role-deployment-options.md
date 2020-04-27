---
title: Especificando opções de implantação de partição e função | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9b36013f13360a2afcf9546cd1e286b35ae4acd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075348"
---
# <a name="specifying-partition-and-role-deployment-options"></a>Especificando opções de implantação de função e de partição
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] assistente de implantação lê as opções de implantação de partição e \<função do *nome do projeto*> arquivo. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]cria esse arquivo quando você compila o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa as opções de implantação de partição e função do projeto atual quando \<o *nome do projeto*> arquivo. deploymentoptions é criado. Para obter mais informações sobre parâmetros de configuração, consulte [Understanding the Input Files Used to Create the Deployment Script](deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Revisando as opções de implantação de partição e de função  
 As opções de implantação no \<arquivo de *nome do projeto*>. deploymentoptions incluem o seguinte:  
  
 **Opções de implantação de partição**  
 O \< *nome do projeto*> arquivo. deploymentoptions especifica se as partições existentes no banco de dados de destino são retidas ou substituídas (padrão). Se as partições existentes forem retidas, só serão implantadas partições novas e os projetos de partições e agregação em todos os grupos de medidas existentes ficarão inalterados.  
  
> [!NOTE]  
>  Se o grupo de medidas no qual a partição existe for excluído, a partição será excluída automaticamente.  
  
 **Opções de implantação de função**  
 O \< *nome do projeto*> arquivo. deploymentoptions especifica uma das seguintes opções de implantação de função:  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e apenas novas funções e membros de função são implantados.  
  
-   Todas as funções e os membros de função existentes no banco de dados de destino são substituídos pelas funções e pelos membros sendo implantados.  
  
-   As funções e os membros de função existentes no banco de dados de destino são retidos e nenhuma nova função será implantada.  
  
-   **Nota** Quando funções e membros existentes são retidos, as permissões associadas a essas funções são redefinidas como nenhuma. As permissões de segurança são contidas pelos objetos que protegem, não pelas funções de segurança com que estão associadas. Para obter mais informações sobre como trabalhar com esse comportamento usando o assistente de implantação do Analysis Service, consulte "reter funções e membros" na base de dados de conhecimento Microsoft.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modificando as opções de implantação de partição e de função  
 Talvez seja necessário implantar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto usando opções de partição e função diferentes das armazenadas no arquivo nome \<do *projeto*>. deploymentoptions. Por exemplo, talvez você queira reter partições, funções e membros de função existentes, em vez de substituir todas as partições, funções e membros existentes, conforme indicado no \<arquivo *nome do projeto*>. deploymentoptions.  
  
 Para modificar a implantação de partições e funções em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projeto do, você não pode alterar as configurações de partição e funções no projeto porque a caixa de diálogo * \<nome do projeto>* **páginas de propriedades** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não exibe essas opções. Se você quiser alterar as opções de implantação para funções e partições, deverá alterar essas informações dentro do \< *nome do projeto*>. deploymentoptions próprio arquivo. O procedimento a seguir descreve como alterar as opções de implantação de partição e de \<função dentro do *nome do projeto*> arquivo. deploymentoptions.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Para alterar a implantação de partições ou de funções depois que os arquivos de entrada tiverem sido gerados  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interativamente, e na página **Opções de implantação de partição e de função** , especifique as novas opções de implantação para as partições e funções.  
  
     -ou-  
  
-   Execute o Assistente para Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no prompt de comando e defina o assistente para ser executado em modo de arquivo de resposta. (Para obter mais informações sobre o modo de arquivo de resposta, consulte [executando o assistente de implantação de Analysis Services](running-the-analysis-services-deployment-wizard.md).)  
  
     -ou-  
  
-   Abra o \< *nome do projeto*>. deploymentoptions em qualquer editor de texto e altere manualmente as opções.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando o destino de instalação](deployment-script-files-specifying-the-installation-target.md)   
 [Especificando definições de configuração para implantação de solução](deployment-script-files-solution-deployment-config-settings.md)   
 [Especificando opções de processamento](deployment-script-files-specifying-processing-options.md)  
  
  
