---
title: Criar um utilitário de implantação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- deploying packages [Integration Services], deployment utility
- deployment utility [Integration Services]
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c725218ac66be169d59f2b32f42e156361b13a51
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392854"
---
# <a name="create-a-deployment-utility"></a>Criar um utilitário de implantação
  A primeira etapa da implantação de pacotes é a criação de um utilitário de implantação para um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O utilitário de implantação é uma pasta que contém os arquivos necessários para a implantação dos pacotes em um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um servidor diferente. O utilitário de implantação é criado no computador no qual o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é armazenado.  
  
 Você cria um utilitário de implantação de pacotes para um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] configurando primeiro o processo de compilação para criar um utilitário de implantação e, depois, compilando o projeto. Quando você compila o projeto, todos os pacotes e configurações de pacote do projeto são incluídos automaticamente. Para implantar arquivos adicionais como um arquivo Leiame com o projeto, coloque os arquivos na pasta **Diversos** do projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Quando o projeto é compilado, esses arquivos também são automaticamente incluídos.  
  
 Você pode configurar cada implantação de projeto de modo diferente. Antes de compilar o projeto e criar o utilitário de implantação do pacote, você pode definir as propriedades no utilitário de implantação para personalizar o modo como os pacotes do projeto serão implantados. Por exemplo, você pode especificar se as configurações do pacote podem ser atualizadas quando o projeto é implantado. Para acessar as propriedades de um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
 A tabela a seguir lista as propriedades do utilitário de implantação.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|AllowConfigurationChange|Um valor que especifica se as configurações podem ser atualizadas durante a implantação.|  
|CreateDeploymentUtility|Um valor que especifica se um utilitário de implantação do pacote é criado quando o projeto é compilado. Essa propriedade deve ser `True` para criar um utilitário de implantação.|  
|DeploymentOutputPath|O local, relativo ao projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , do utilitário de implantação.|  
  
 Quando você cria um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], um arquivo de manifesto, \<project name>.SSISDeploymentManifest.xml, é criado e adicionado, junto com cópias dos pacotes de projeto e dependências do pacote, à pasta bin\Deployment do projeto ou ao local especificado na propriedade DeploymentOutputPath. O arquivo de manifesto lista os pacotes, as configurações de pacote e os diversos arquivos do projeto.  
  
 O conteúdo da pasta de implantação é atualizado toda vez que você compila o projeto. Isso significa que qualquer arquivo salvo nessa pasta que não for copiado novamente na pasta pelo processo de compilação será excluído. Por exemplo, serão excluídos arquivos de configuração do pacote salvos nas pastas de implantação.  
  
### <a name="to-create-a-package-deployment-utility"></a>Para criar um utilitário de implantação de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução que contém o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para o qual você quer criar um utilitário de implantação de pacote.  
  
2.  Clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Páginas de Propriedades do \<project name>**, clique em **Utilitário de Implantação**.  
  
4.  Para atualizar as configurações do pacote quando os pacotes são implantados, defina **AllowConfigurationChanges** para `True`.  
  
5.  Defina `CreateDeploymentUtility` como `True`.  
  
6.  Opcionalmente, atualize o local do utilitário de implantação modificando a propriedade do `DeploymentOutputPath`.  
  
7.  Clique em **OK**.  
  
8.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Criar**.  
  
9. Visualize o progresso da compilação e os erros de compilação na janela **Saída** .  
  
## <a name="see-also"></a>Consulte também  
 [Configurações do Pacote](../../2014/integration-services/package-configurations.md)   
 [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md)   
 [Implantar pacotes por meio do utilitário de implantação](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)   
 [Implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
