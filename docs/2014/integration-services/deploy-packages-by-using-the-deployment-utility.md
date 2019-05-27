---
title: Implantar pacotes usando o utilitário de implantação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73b71e83f3b0f0f895b2cc5b8fd3495fb4893a32
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059618"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>Implantar pacotes usando o utilitário de implantação
  Quando você cria um utilitário de implantação para instalar pacotes de um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador diferente daquele em que o utilitário de implantação foi criado, é necessário primeiro copiar a pasta de implantação no computador de destino.  
  
 O caminho da pasta de implantação está especificado na propriedade DeploymentOutputPath do projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para o qual foi criado o utilitário de implantação. O caminho padrão é bin\Deployment, relativo ao projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Criar um utilitário de implantação](../../2014/integration-services/create-a-deployment-utility.md).  
  
 É possível usar o Assistente de Instalação de Pacotes para instalar os pacotes. Para iniciar o assistente, clique duas vezes no arquivo do utilitário de implantação depois de ter copiado a pasta de implantação no servidor. Esse arquivo é chamado \<project name>.SSISDeploymentManifest e pode ser encontrado na pasta de implantação do computador de destino.  
  
> [!NOTE]  
>  Dependendo da versão do pacote que está sendo implantado, você poderá encontrar um erro se tiver diferentes versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instaladas lado a lado. Esse erro pode ocorrer porque a extensão do nome de arquivo .SSISDeploymentManifest é a mesma para todas as versões do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Clicar duas vezes no arquivo chama o instalador (dtsinstall.exe) da versão instalada mais recentemente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], que talvez não seja a mesma versão do arquivo de utilitário de implantação. Para resolver esse problema, execute a versão correta de dtsinstall.exe na linha de comando e forneça o caminho do arquivo de utilitário de implantação.  
  
 O Assistente de Instalação de Pacotes o guiará pelas etapas para instalar pacotes no sistema de arquivos ou no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você pode configurar a instalação das seguintes formas:  
  
-   Escolhendo o local e o tipo de local para instalar os pacotes.  
  
-   Escolhendo o local para instalar dependências dos pacotes.  
  
-   Validando os pacotes após a instalação no servidor de destino.  
  
 As dependências com base em arquivo para pacotes sempre são instaladas no sistema de arquivos. Se for instalado um pacote no sistema de arquivos, as dependências serão instaladas na mesma pasta especificada por você para o pacote. Se instalar um pacote em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você poderá especificar a pasta na qual armazenará as dependências com base no arquivo.  
  
 Se o pacote incluir configurações que deseja modificar para usar no computador destino, você poderá atualizar os valores e as propriedades usando o assistente.  
  
 Além de instalar os pacotes com o Assistente de Instalação de Pacotes, você pode copiar e mover pacotes com o utilitário de prompt de comando **dtutil** . Para obter mais informações, consulte [dtutil Utility](dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>Para implantar pacotes em uma instância do SQL Server  
  
1.  Abra a pasta de implantação no computador de destino.  
  
2.  Clique duas vezes no arquivo de manifesto, \<project name>.SSISDeploymentManifest, para iniciar o Assistente de Instalação de Pacotes.  
  
3.  Na página **Implantar Pacotes SSIS** , selecione a opção **Implantação no SQL Server** .  
  
4.  Opcionalmente, selecione **Validar pacotes após instalação** para validar os pacotes depois de instalados no servidor de destino.  
  
5.  Na página **Especificar SQL Server de Destino** , especifique a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para instalar os pacotes e selecionar um modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , precisará fornecer um nome de usuário e uma senha.  
  
6.  Na página **Selecionar Pasta de Instalação** , especifique a pasta no sistema de arquivos para as dependências do pacote que serão instaladas.  
  
7.  Se o pacote incluir configurações, você poderá editar as configurações atualizando os valores na lista **Valor** da página Configurar Pacotes.  
  
8.  Se você escolheu validar os pacotes após a instalação, exiba os resultados de validação dos pacotes implantados.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
