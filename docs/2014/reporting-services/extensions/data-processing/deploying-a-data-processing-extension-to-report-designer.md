---
title: 'Como: Implantar uma extensão de processamento de dados no Designer de relatórios | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ded3d366450ab3d5ea3375bb02929b4b52337d0f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011558"
---
# <a name="how-to-deploy-a-data-processing-extension-to-report-designer"></a>Como: Implantar uma extensão de processamento de dados no Designer de relatórios
  O Designer de Relatórios usa extensões de processamento de dados para recuperar e processar dados enquanto você estiver criando relatórios. Você deve implantar o seu assembly de extensão de processamento de dados para o Designer de Relatórios como um assembly privado. Precisa também criar uma uma entrada no arquivo de configuração do Designer de Relatórios, RSReportDesigner.config.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>Para implantar um assembly de extensão de processamento de dados  
  
1.  Copie o assembly de seu local de preparação para o diretório do Designer de Relatórios. O local padrão do diretório do Designer de Relatórios é C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
2.  Depois de copiar o arquivo de assembly, abra o arquivo RSReportDesigner.config. O arquivo RSReportDesigner.config também está localizado no diretório do Designer de Relatórios. Você precisa criar uma entrada no arquivo de configuração para o seu arquivo de assembly de extensão de processamento de dados. Abra o arquivo de configuração com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou com um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **Data** no arquivo RSReportDesigner.config. Uma entrada para a extensão de processamento de dados recém-criada deve ser adicionada no seguinte local:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Adicionar uma entrada para a sua extensão de processamento de dados que inclui um **extensão** elemento com valores para o `Name`, `Type`, e `Visible` atributos. A sua entrada poderia ser assim:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     O valor de `Name` é o nome exclusivo da extensão de processamento de dados. O valor de `Type` é uma lista separada por vírgulas que inclui uma entrada para o namespace totalmente qualificado da sua classe que implementa as interfaces <xref:Microsoft.ReportingServices.Interfaces.IExtension> e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>, seguida do nome do seu assembly (sem incluir a extensão de arquivo .dll). Por padrão, as extensões de processamento de dados estão visíveis. Para ocultar uma extensão de interfaces do usuário, como o Designer de relatórios, adicione uma `Visible` de atributo para o **extensão** elemento e defina-o como `false`.  
  
5.  Por fim, adicione um grupo de códigos ao assembly personalizado que concede a permissão **FullTrust** para a extensão. Faça isso adicionando o grupo de códigos ao arquivo rspreviewpolicy.config localizado por padrão em C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies. O grupo de códigos pode ter esta aparência:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 A associação da URL é somente uma das condições de associação que você pode escolher para a sua extensão de processamento de dados. Para obter mais informações sobre a segurança de acesso do código no [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)], consulte [Desenvolvimento seguro &#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>Designer de consulta genérico  
 O Designer de Relatórios oferece um designer de consulta genérico que você pode usar com extensões de processamento de dados personalizadas. Esse designer consiste em dois painéis: um painel de consulta e um painel de resultados. Você pode usar o designer genérico para escrever consultas que não são suportadas pela interface gráfica. Ao contrário do designer de consultas gráficas, o designer de consulta genérico não verifica a sintaxe da consulta ou a reestrutura.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>Para habilitar o designer de consulta genérico para uma extensão personalizada.  
  
-   Adicione a seguinte entrada ao arquivo RSReportDesigner config sob o **Designer** elemento, substituindo o `Name` atributo com o nome que você forneceu nas entradas anteriores.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Antes de verificar a implantação, é preciso fechar todas as instâncias do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] no computador local. Depois de encerrar todas as sessões atuais, você poderá verificar se a extensão de processamento de dados foi implantada com êxito para o Designer de Relatórios criando um novo projeto de relatório no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. A sua extensão deve ser incluída na lista de tipos de fontes de dados disponíveis quando você criar um novo conjunto de dados para o relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Implantando uma extensão de processamento de dados](deploying-a-data-processing-extension.md)   
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
