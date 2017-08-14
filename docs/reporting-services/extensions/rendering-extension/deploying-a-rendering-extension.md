---
title: "Implantando uma extensão de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
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
- deploying [Reporting Services], extensions
- rendering extensions [Reporting Services], deploying
ms.assetid: 9fb8c887-5cb2-476e-895a-7b0e2dd11398
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 3fbab7c48a0d522519a9e7ada9cf9c8cb1d40c7b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="deploying-a-rendering-extension"></a>Implantando uma extensão de renderização
  Depois de ter escrito e compilado sua [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatar extensão de renderização em um [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] biblioteca, você precisa torná-lo detectável pelo servidor de relatório e pelo Designer de relatórios. Para fazer isso, copie a extensão para o diretório apropriado e adicione entradas para os arquivos de configuração [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] apropriados.  
  
## <a name="configuration-file-rendering-extension-element"></a>Elemento de extensão de renderização de arquivo de configuração  
 Quando uma extensão de renderização foi compilada em um .DLL, você adiciona uma entrada no arquivo rsreportserver.config. Por padrão, o local é %ProgramFiles%\Microsoft SQL Server\MSRS10_50. \<InstanceName > services\reportserver. O elemento pai é \<renderizar >. Sob o elemento Render, existe um elemento Extension para cada extensão de renderização. O elemento **Extension** contém dois atributos, Name e Type.  
  
 A tabela a seguir descreve os atributos para o elemento **Extension** para as extensões de renderização:  
  
|Atributo|Description|  
|---------------|-----------------|  
|**Nome**|Um nome exclusivo para a extensão. O tamanho máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas do elemento **Extension** de um arquivo de configuração. Se um nome duplicado estiver presente, o servidor de relatório retornará um erro.|  
|**Tipo**|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|**Visível**|Um valor **false** indica que a extensão de renderização não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será **true**.|  
|**LogAllExecutionRequests**|Um valor de **false** indica que uma entrada está registrada apenas para a primeira execução do relatório em uma sessão. Se o atributo não for incluído, o valor padrão será **true**.<br /><br /> Esta configuração determina, por exemplo, se é preciso registrar uma entrada apenas para a primeira página renderizada de um relatório (quando **false**) ou uma entrada para cada página renderizada do relatório (quando **true**).|  
  
 Para obter mais informações, consulte [Arquivo de configuração RsReportServer.config](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Implantando a extensão para o Servidor de Relatório  
 O servidor de relatório usa extensões de renderização para exportar relatórios para outros formatos. Implante o seu assembly de extensão de renderização para o servidor de relatório como um assembly privado. Também será preciso criar uma entrada no arquivo de configuração do servidor de relatório, rsreportserver.config.  
  
### <a name="to-deploy-the-assembly"></a>Para implantar o assembly  
  
1.  Copie o assembly do local de preparação para o diretório bin do servidor de relatório no qual você deseja usar a extensão de renderização. O local padrão do diretório Bin do servidor de relatório é %ProgramFiles%\Microsoft SQL Server\MSRS10_50. \<InstanceName > Services\ReportServer\bin.  
  
2.  Depois da cópia do arquivo de assembly, abra o arquivo rsreportserver.config. O arquivo rsreportserver.config também está localizado no diretório bin do servidor de relatório. Você precisa criar uma entrada no arquivo de configuração para o seu arquivo de assembly de extensão. Você pode abrir o arquivo com [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou um editor de texto simples.  
  
     Para obter mais informações, consulte [Arquivo de configuração RsReportServer.config](../../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
3.  Localize o elemento **Render** no arquivo Rsreportserver.config. Uma entrada para a sua extensão recém-criada deve ser inserida no seguinte local:  
  
    ```  
    <Extensions>  
       <Render>  
          <extension configuration>  
       </Render>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para sua extensão de renderização. A sua entrada deve incluir um elemento que possui valores para **Name** e **Type**e poderia ser assim:  
  
    ```  
    <Extension Name="My Rendering Extension Name" Type="CompanyName.ExtensionName.MyRenderingProvider, AssemblyName" />  
    ```  
  
     O valor de **Name** é o nome exclusivo da extensão de renderização. O valor de **tipo** é uma lista separada por vírgulas que inclui uma entrada para o namespace totalmente qualificado da sua <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> implementação, seguida do nome do seu assembly (não incluindo a extensão de arquivo. dll). Por padrão, as extensões de renderização ficam visíveis. Para ocultar uma extensão de interfaces do usuário, como o Gerenciador de Relatórios, adicione um atributo **Visible** ao elemento **Extension** e defina-o como **false**.  
  
## <a name="verifying-the-deployment"></a>Verificando a implantação  
 Você também pode abrir o Gerenciador de Relatórios e verificar se a sua extensão foi incluída na lista de tipos de exportação disponíveis para um relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Visão geral de extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementando a Interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Considerações de segurança para extensões](../../../reporting-services/extensions/security-considerations-for-extensions.md)  
  
  
