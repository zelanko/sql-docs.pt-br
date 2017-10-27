---
title: "Como: implantar uma extensão de processamento de dados no Designer de relatórios | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e5e309ee7092bdc64efa89fa27579e9e8944da14
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension-to-report-designer"></a>Implantando uma extensão de processamento de dados para o Designer de relatórios
  O Designer de Relatórios usa extensões de processamento de dados para recuperar e processar dados enquanto você estiver criando relatórios. Você deve implantar o seu assembly de extensão de processamento de dados para o Designer de Relatórios como um assembly privado. Precisa também criar uma uma entrada no arquivo de configuração do Designer de Relatórios, RSReportDesigner.config.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>Para implantar um assembly de extensão de processamento de dados  
  
1.  Copie o assembly de seu local de preparação para o diretório do Designer de Relatórios. O local padrão do diretório do Designer de Relatórios é C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
2.  Depois de copiar o arquivo de assembly, abra o arquivo RSReportDesigner.config. O arquivo RSReportDesigner.config também está localizado no diretório do Designer de Relatórios. Você precisa criar uma entrada no arquivo de configuração para o seu arquivo de assembly de extensão de processamento de dados. Você pode abrir o arquivo de configuração com [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou com um editor de texto simples, como o bloco de notas.  
  
3.  Localize o elemento **Data** no arquivo RSReportDesigner.config. Uma entrada para a extensão de processamento de dados recém-criada deve ser adicionada no seguinte local:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para a sua extensão de processamento de dados que inclui um **extensão** elemento com valores para o **nome**, **tipo**, e **visível** atributos. A sua entrada poderia ser assim:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     O valor de **nome** é o nome exclusivo da extensão de processamento de dados. O valor de **tipo** é uma lista separada por vírgulas que inclui uma entrada para o namespace totalmente qualificado da sua classe que implementa o <xref:Microsoft.ReportingServices.Interfaces.IExtension> e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> interfaces, seguidos do nome do seu assembly (não incluindo a extensão de arquivo. dll). Por padrão, as extensões de processamento de dados estão visíveis. Para ocultar uma extensão de interfaces do usuário, como o Designer de relatórios, adicione um **visível** de atributo para o **extensão** elemento e defina-a como **false**.  
  
5.  Finalmente, adicione um grupo de códigos para seu assembly personalizado que concede **FullTrust** permissão para a sua extensão. Faça isso adicionando o grupo de códigos ao arquivo rspreviewpolicy.config localizado por padrão em C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies. O grupo de códigos pode ter esta aparência:  
  
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
  
 A associação da URL é somente uma das condições de associação que você pode escolher para a sua extensão de processamento de dados. Para obter mais informações sobre a segurança de acesso do código em [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)], consulte [desenvolvimento seguro &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>Designer de consulta genérico  
 O Designer de Relatórios oferece um designer de consulta genérico que você pode usar com extensões de processamento de dados personalizadas. Esse designer consiste em dois painéis: um painel de consulta e um painel de resultados. Você pode usar o designer genérico para escrever consultas que não são suportadas pela interface gráfica. Ao contrário do designer de consultas gráficas, o designer de consulta genérico não verifica a sintaxe da consulta ou a reestrutura.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>Para habilitar o designer de consulta genérico para uma extensão personalizada.  
  
-   Adicione a seguinte entrada ao arquivo RSReportDesigner. config sob o **Designer** elemento, substituindo o **nome** atributo com o nome que você forneceu nas entradas anteriores.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Antes de verificar a implantação, é preciso fechar todas as instâncias do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] no computador local. Depois de encerrar todas as sessões atuais, você poderá verificar se a extensão de processamento de dados foi implantada com êxito para o Designer de Relatórios criando um novo projeto de relatório no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. A sua extensão deve ser incluída na lista de tipos de fontes de dados disponíveis quando você criar um novo conjunto de dados para o relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Implantando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

