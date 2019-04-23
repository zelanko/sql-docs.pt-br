---
title: 'Como fazer: Implantar uma extensão de processamento de dados para um servidor de relatório | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0f593b2488d9bb7226edad1f8d98a244f4df191
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154212"
---
# <a name="how-to-deploy-a-data-processing-extension-to-a-report-server"></a>Como fazer: Implantar uma extensão de processamento de dados para um servidor de relatório
  Servidores de relatórios usam extensões de processamento de dados por recuperar e processar dados em relatórios renderizados. Você deve implantar o seu assembly de extensão de processamento de dados para um servidor de relatório como um assembly privado. Também será preciso criar uma entrada no arquivo de configuração do servidor de relatório, RSReportServer.config.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>Para implantar um assembly de extensão de processamento de dados  
  
1.  Copie o assembly do local de preparo para o diretório bin do servidor de relatório no qual você deseja usar a extensão de processamento de dados. O local padrão do diretório bin do servidor de relatório é %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<*Instance Name*>\Reporting Services\ReportServer\bin.  
  
    > [!NOTE]  
    >  Esta etapa impedirá uma atualização para uma instância mais nova do SQL Server. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](../../install-windows/upgrade-and-migrate-reporting-services.md).  
  
2.  Depois que o arquivo do assembly for copiado, abra o arquivo RSReportServer.config. O arquivo RSReportServer.config está localizado no diretório ReportServer. Você precisa criar uma entrada no arquivo de configuração para o seu arquivo de assembly de extensão de processamento de dados. Abra o arquivo de configuração com o Visual Studio ou com um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento `Data` no arquivo RSReportServer.config. Uma entrada para a extensão de processamento de dados recém-criada deve ser adicionada no seguinte local:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para sua extensão de processamento de dados. A sua entrada deve incluir um elemento `Extension` com valores para `Name` e `Type` e deve ter esta aparência:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     O valor de `Name` é o nome exclusivo da extensão de processamento de dados. O valor de `Type` é uma lista separada por vírgulas que inclui uma entrada para o namespace totalmente qualificado da sua classe que implementa as interfaces <xref:Microsoft.ReportingServices.Interfaces.IExtension> e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>, seguida do nome do seu assembly (sem incluir a extensão de arquivo .dll). Por padrão, as extensões de processamento de dados estão visíveis. Para ocultar uma extensão de interfaces do usuário, como, por exemplo, o Gerenciador de Relatórios, adicione um atributo `Visible` ao elemento `Extension` e defina-o como `false`.  
  
5.  Adicione um grupo de códigos ao seu assembly personalizado que concede permissão `FullTrust` para a sua extensão. Faça isso adicionando o grupo de códigos ao arquivo rssrvpolicy.config localizado, por padrão, em %ProgramFiles%\Microsoft SQL Server\\<MSRS10_50.\<*Instance Name*>\Reporting Services\ReportServer. O grupo de códigos pode ter esta aparência:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<Instance Name>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 A associação da URL é somente uma das condições de associação que você pode escolher para a sua extensão de processamento de dados. Para obter mais informações sobre a segurança de acesso do código no [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte [Desenvolvimento seguro &#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md).  
  
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Você pode verificar se sua extensão de processamento de dados foi implantada com êxito no servidor de relatório usando o método <xref:ReportService2010.ReportingService2010.ListExtensions%2A> do serviço Web. Você também pode abrir o Gerenciador de Relatórios e verificar se a sua extensão foi incluída na lista de fontes de dados disponíveis. Para obter mais informações sobre o Gerenciador de Relatórios e fontes de dados, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implantando uma extensão de processamento de dados](deploying-a-data-processing-extension.md)   
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
