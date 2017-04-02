---
title: "Implantar pacotes por meio do utilit&#225;rio de implanta&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes [Integration Services], instalando"
  - "instalando pacotes"
  - "dependências [Integration Services]"
  - "implantação de pacotes [Integration Services], instalando"
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
caps.latest.revision: 57
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Implantar pacotes por meio do utilit&#225;rio de implanta&#231;&#227;o
  Quando você cria um utilitário de implantação para instalar pacotes de um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador diferente daquele em que o utilitário de implantação foi criado, é necessário primeiro copiar a pasta de implantação no computador de destino.  
  
 O caminho da pasta de implantação está especificado na propriedade DeploymentOutputPath do projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o qual foi criado o utilitário de implantação. O caminho padrão é bin\Deployment, relativo ao projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Criar um utilitário de implantação](../../integration-services/packages/create-a-deployment-utility.md).  
  
 É possível usar o Assistente de Instalação de Pacotes para instalar os pacotes. Para iniciar o assistente, clique duas vezes no arquivo do utilitário de implantação depois de ter copiado a pasta de implantação no servidor. Este arquivo é chamado \<nome do projeto>.SSISDeploymentManifest e pode ser localizado na pasta de implantação no computador de destino.  
  
> [!NOTE]  
>  Dependendo da versão do pacote que está sendo implantado, você poderá encontrar um erro se tiver diferentes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas lado a lado. Esse erro pode ocorrer porque a extensão do nome de arquivo .SSISDeploymentManifest é a mesma para todas as versões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Clicar duas vezes no arquivo chama o instalador (dtsinstall.exe) da versão instalada mais recentemente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que talvez não seja a mesma versão do arquivo de utilitário de implantação. Para resolver esse problema, execute a versão correta de dtsinstall.exe na linha de comando e forneça o caminho do arquivo de utilitário de implantação.  
  
 O Assistente de Instalação de Pacotes o guiará pelas etapas para instalar pacotes no sistema de arquivos ou no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode configurar a instalação das seguintes formas:  
  
-   Escolhendo o local e o tipo de local para instalar os pacotes.  
  
-   Escolhendo o local para instalar dependências dos pacotes.  
  
-   Validando os pacotes após a instalação no servidor de destino.  
  
 As dependências com base em arquivo para pacotes sempre são instaladas no sistema de arquivos. Se for instalado um pacote no sistema de arquivos, as dependências serão instaladas na mesma pasta especificada por você para o pacote. Se instalar um pacote em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá especificar a pasta na qual armazenará as dependências com base no arquivo.  
  
 Se o pacote incluir configurações que deseja modificar para usar no computador destino, você poderá atualizar os valores e as propriedades usando o assistente.  
  
 Além de instalar os pacotes com o Assistente de Instalação de Pacotes, você pode copiar e mover pacotes com o utilitário de prompt de comando **dtutil**. Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### Para implantar pacotes em uma instância do SQL Server  
  
1.  Abra a pasta de implantação no computador de destino.  
  
2.  Clique duas vezes no arquivo de manifesto, \<nome do projeto>.SSISDeploymentManifest, para iniciar o Assistente de Instalação de Pacotes.  
  
3.  Na página **Implantar Pacotes SSIS**, selecione a opção **Implantação no SQL Server**.  
  
4.  Opcionalmente, selecione **Validar pacotes após instalação** para validar os pacotes depois de instalados no servidor de destino.  
  
5.  Na página **Especificar SQL Server de Destino**, especifique a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar os pacotes e selecionar um modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], precisará fornecer um nome de usuário e uma senha.  
  
6.  Na página **Selecionar Pasta de Instalação**, especifique a pasta no sistema de arquivos para as dependências do pacote que serão instaladas.  
  
7.  Se o pacote incluir configurações, você poderá editar as configurações atualizando os valores na lista **Valor** da página Configurar Pacotes.  
  
8.  Se você escolheu validar os pacotes após a instalação, exiba os resultados de validação dos pacotes implantados.  
  
## Consulte também  
 [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  