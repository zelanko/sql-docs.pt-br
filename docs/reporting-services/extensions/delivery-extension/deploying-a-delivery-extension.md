---
title: Implantando uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 99ada408d4f2a783d2a545d00f780763b7a27796
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016363"
---
# <a name="deploying-a-delivery-extension"></a>Implantando uma extensão de entrega
  As extensões de entrega fornecem suas informações de configuração na forma de um arquivo de configuração XML. O arquivo XML é compatível com o esquema XML definido para extensões de entrega. As extensões de entrega oferecem infraestrutura para a definição e para a modificação do arquivo de configuração.  
  
 Se uma extensão de entrega for substituída ou atualizada, todas as assinaturas que a referenciam permanecerão válidas.  
  
 Depois de escrever e compilar sua extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] em uma biblioteca do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você deve copiar a extensão para o diretório apropriado e adicionar uma entrada ao arquivo de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adequado para que o servidor de relatório possa localizá-lo.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extensão do arquivo de configuração  
 As extensões de entrega que você implanta no servidor de relatório precisam ser inseridas como elementos **Extension** no arquivo de configuração. O arquivo de configuração para o servidor de relatório é RSReportServer.config.  
  
 A tabela a seguir descreve os atributos do elemento **Extension** em extensões de entrega.  
  
|attribute|Description|  
|---------------|-----------------|  
|**Nome**|Um nome exclusivo para a extensão (por exemplo "Email do Servidor de Relatório" para a extensão de entrega de email ou "FileShare do Servidor de Relatório" para a extensão de entrega do compartilhamento de arquivo). O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração. Se um nome duplicado estiver presente, o servidor de relatório retornará um erro.|  
|**Tipo**|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|**Visível**|Um valor igual a **false** indica que a extensão de entrega não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será **true**.|  
  
 Para obter mais informações sobre o arquivo RSReportServer.config, consulte [Arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implantando a extensão para o Servidor de Relatório  
 O servidor de relatório usa extensões de entrega para processamento e entrega de notificações ou de relatórios. Implante o seu assembly de extensão de entrega para o servidor de relatório como um assembly privado. Também será preciso criar uma entrada no arquivo de configuração do servidor de relatório, RSReportServer.config.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>Para implantar um assembly de extensão de entrega para um servidor de relatório  
  
1.  Copie o assembly do local de preparação para o diretório bin do servidor de relatório no qual você deseja usar a extensão de entrega. A localização padrão do diretório bin do servidor de relatório é %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer\bin.  
  
    > [!IMPORTANT]  
    >  Se você estiver tentando substituir um assembly de extensão de entrega existente, primeiro deverá parar o serviço Servidor de Relatório antes de copiar o assembly atualizado. Reinicie o seu serviço depois de terminar de copiar o assembly.  
  
2.  Depois que o arquivo do assembly for copiado, abra o arquivo RSReportServer.config. O arquivo RSReportServer.config está localizado no diretório %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer. É necessário criar uma entrada no arquivo de configuração para o arquivo de assembly de extensão de entrega. Abra o arquivo de configuração com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **Delivery** no arquivo RSReportServer.config. Uma entrada para a sua extensão de entrega recém-criada deve ser feita no seguinte local:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para a sua extensão de entrega. A entrada deve incluir um elemento **Extension** com valores para **Name** e **Type** e poderá ser assim:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     O valor de **Name** é o nome exclusivo da extensão de entrega. O valor de **Type** é uma lista separada por vírgula que inclui uma entrada para o namespace totalmente qualificado da classe que implementa a interface <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>, seguida pelo nome do assembly (não incluindo a extensão de arquivo .dll). Por padrão, as extensões de entrega ficam visíveis. Para ocultar uma extensão de interfaces do usuário, como o portal da Web, adicione um atributo **Visible** ao elemento **Extension** e defina-o como **false**.  
  
5.  Por fim, adicione um grupo de códigos ao assembly personalizado que concede a permissão **FullTrust** para a extensão de entrega. Faça isso adicionando o grupo de códigos ao arquivo rssrvpolicy.config localizado por padrão em %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer. O grupo de códigos pode ter esta aparência:  
  
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
  
     A associação da URL é somente uma das condições de associação que você pode escolher para a sua extensão de entrega. Para obter mais informações sobre a segurança de acesso do código no [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], consulte [Desenvolvimento seguro &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Você pode verificar se sua extensão de entrega foi implantada com êxito no servidor de relatório usando o método <xref:ReportService2010.ReportingService2010.ListExtensions%2A> do serviço Web. Você também pode abrir o portal da Web e verificar se a extensão foi incluída na lista de extensões de entrega disponíveis para uma assinatura. Para obter mais informações sobre o portal da Web e assinaturas, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
