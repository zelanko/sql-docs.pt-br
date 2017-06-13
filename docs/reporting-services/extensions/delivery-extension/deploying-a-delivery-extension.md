---
title: "Implantando uma extensão de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d072577828375a08c133bb1a68d93e652e5cf168
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-delivery-extension"></a>Implantando uma extensão de entrega
  As extensões de entrega fornecem suas informações de configuração na forma de um arquivo de configuração XML. O arquivo XML é compatível com o esquema XML definido para extensões de entrega. As extensões de entrega oferecem infraestrutura para a definição e para a modificação do arquivo de configuração.  
  
 Se uma extensão de entrega for substituída ou atualizada, todas as assinaturas que a referenciam permanecerão válidas.  
  
 Depois de ter escrito e compilado sua [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de entrega em uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] biblioteca, você deve copiar a extensão para o diretório apropriado e adicione uma entrada apropriada [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] arquivo de configuração para o servidor de relatório possa localizá-lo.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extensão do arquivo de configuração  
 Extensões de entrega que você implantar o servidor de relatório devem ser inseridas como **extensão** elementos no arquivo de configuração. O arquivo de configuração para o servidor de relatório é RSReportServer.config.  
  
 A tabela a seguir descreve os atributos para o **extensão** elemento para extensões de entrega.  
  
|Atributo|Description|  
|---------------|-----------------|  
|**Nome**|Um nome exclusivo para a extensão (por exemplo "Email do Servidor de Relatório" para a extensão de entrega de email ou "FileShare do Servidor de Relatório" para a extensão de entrega do compartilhamento de arquivo). O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração. Se um nome duplicado estiver presente, o servidor de relatório retornará um erro.|  
|**Tipo**|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|**Visível**|Um valor de **false** indica que a extensão de entrega não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será **true**.|  
  
 Para obter mais informações sobre o arquivo rsreportserver. config, consulte [arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implantando a extensão para o Servidor de Relatório  
 O servidor de relatório usa extensões de entrega para processamento e entrega de notificações ou de relatórios. Implante o seu assembly de extensão de entrega para o servidor de relatório como um assembly privado. Também será preciso criar uma entrada no arquivo de configuração do servidor de relatório, RSReportServer.config.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>Para implantar um assembly de extensão de entrega para um servidor de relatório  
  
1.  Copie o assembly do local de preparação para o diretório bin do servidor de relatório no qual você deseja usar a extensão de entrega. O local padrão do diretório bin do servidor de relatório é %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > Services\ReportServer\bin..  
  
    > [!IMPORTANT]  
    >  Se você estiver tentando substituir um assembly de extensão de entrega existente, primeiro deverá parar o serviço Servidor de Relatório antes de copiar o assembly atualizado. Reinicie o seu serviço depois de terminar de copiar o assembly.  
  
2.  Depois que o arquivo do assembly for copiado, abra o arquivo RSReportServer.config. O arquivo rsreportserver. config está localizado em %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > services\reportserver. directory. É necessário criar uma entrada no arquivo de configuração para o arquivo de assembly de extensão de entrega. Você pode abrir o arquivo de configuração com [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou um editor de texto simples, como o bloco de notas.  
  
3.  Localize o **entrega** elemento no arquivo rsreportserver. config. Uma entrada para a sua extensão de entrega recém-criada deve ser feita no seguinte local:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para a sua extensão de entrega. Sua entrada deve incluir um **extensão** elemento com valores para **nome** e **tipo**e pode parecer com o seguinte:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     O valor de **nome** é o nome exclusivo da extensão de entrega. O valor de **tipo** é uma lista separada por vírgulas que inclui uma entrada para o namespace totalmente qualificado da sua classe que implementa o <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> interface, seguido do nome do seu assembly (não incluindo a extensão de arquivo. dll). Por padrão, as extensões de entrega ficam visíveis. Para ocultar uma extensão de interfaces do usuário, como o portal da web, adicione um **visível** de atributo para o **extensão** elemento e defina-a como **false**.  
  
5.  Finalmente, adicione um grupo de códigos para seu assembly personalizado que concede **FullTrust** permissão para a sua extensão de entrega. Você pode fazer isso adicionando o grupo de códigos ao arquivo rssrvpolicy. config localizado por padrão em %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > services\reportserver.. O grupo de códigos pode ter esta aparência:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     A associação da URL é somente uma das condições de associação que você pode escolher para a sua extensão de entrega. Para obter mais informações sobre a segurança de acesso do código em [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], consulte.[ Proteger o desenvolvimento de &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Você pode verificar se sua extensão de entrega foi implantada com êxito no servidor de relatório usando o método <xref:ReportService2010.ReportingService2010.ListExtensions%2A> do serviço Web. Você também pode abrir o portal da web e verificar se sua extensão foi incluída na lista de extensões de entrega disponíveis para uma assinatura. Para obter mais informações sobre o portal da web e assinaturas, consulte [assinaturas e entrega &#40; Reporting Services &#41; ](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

