---
title: Executar um pacote no SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ae5924e5fc1cad91b5e1511c61556ece70138dcb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964542"
---
# <a name="run-a-package-in-sql-server-data-tools"></a>Executar um pacote no SQL Server Data Tools
  Normalmente, os pacotes são executados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] durante o desenvolvimento, a depuração e o teste dos pacotes. Quando você executa um pacote no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , o pacote é sempre executado imediatamente.  
  
 Enquanto um pacote está em execução, [!INCLUDE[ssIS](../includes/ssis-md.md)] o designer exibe o progresso da execução do pacote na guia **progresso** . Você pode exibir a hora de início e de término do pacote e suas tarefas e contêineres, além de informações sobre quaisquer tarefas ou contêineres no pacote que falharam. Depois que o pacote terminar a execução, as informações de tempo de execução permanecerão disponíveis na guia **resultados da execução** . Para obter mais informações, consulte a seção "andamento do relatório" no tópico [Depurando o fluxo de controle](control-flow/control-flow.md).  
  
 **Implantação de tempo de design**. Quando um pacote é executado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], ele é criado e, em seguida, implantado em uma pasta. Antes de executar o pacote, você pode especificar a pasta na qual ele será implantado. Por padrão, se você não especificar uma pasta, a pasta **bin** será usada. Este tipo de implantação é chamado de implantação de tempo de design.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>Para executar um pacote nas Ferramentas de Dados do SQL Server  
  
1.  No Gerenciador de Soluções, se sua solução contiver vários projetos, clique com o botão direito do mouse no projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote e clique em **Definir como Objeto de Inicialização** para definir o projeto de inicialização.  
  
2.  No Gerenciador de Soluções, se o projeto contiver vários pacotes, clique com o botão direito do mouse em um pacote e clique em **Definir como Objeto de Inicialização** para definir o pacote de inicialização.  
  
3.  Para executar um pacote, use um dos seguintes procedimentos:  
  
    -   Abra o pacote que você deseja executar e clique em **Iniciar Depuração** na barra de menus ou pressione F5. Após a execução do pacote, pressione Shift+F5 para retornar ao modo de design.  
  
    -   No Gerenciador de Soluções, clique com o botão direito do mouse no pacote e, em seguida, clique em **Executar Pacote**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>Para especificar uma pasta diferente para implantação em tempo de design  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta de projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que você deseja executar e clique em **Propriedades**.  
  
2.  Na caixa de diálogo ** \<project name> páginas de propriedades** , clique em **Compilar**.  
  
3.  Atualize o valor na propriedade OutputPath para especificar a pasta que você deseja usar para a implantação em tempo de design e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)   
 [Pacotes do Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
