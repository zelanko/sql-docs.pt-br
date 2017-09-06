---
title: Implementando a Interface IRenderingExtension | Microsoft Docs
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
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 60eac755180faaba012c7fbd14001fcb66a37975
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-irenderingextension-interface"></a>Implementando a interface IRenderingExtension
  A extensão de renderização obtém os resultados de uma definição de relatório combinada com os dados reais e renderiza os dados resultantes para um formato que seja utilizável. A transformação dos dados combinados e a formatação são feitas usando uma classe CLR (Common Language Runtime) que implementa <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension>. Isto transforma o modelo de objeto em um formato de saída que é consumível por um visualizador, impressora ou outro destino de saída.  
  
 O <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> tem três métodos que devem ser codificados:  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> - renderiza o relatório.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> - renderiza um fluxo específico de um relatório.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>- obtém informações adicionais, como ícones, isso é obrigatório para o relatório.  
  
 As seções a seguir discutem esses métodos em mais detalhes.  
  
## <a name="render-method"></a>Método Render  
 O método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> contém argumentos que representam os seguintes objetos:  
  
-   O *relatório* que você deseja processar. Esse objeto contém propriedades, dados e informações de layout para o relatório. O relatório é a raiz do árvore de modelo de objeto de relatório.  
  
-   O *ServerParameters* que contém o objeto de dicionário de cadeia de caracteres, com os parâmetros para o servidor de relatório, se houver.  
  
-   O *deviceInfo* parâmetro que contêm as configurações do dispositivo. Para obter mais informações, consulte [passando configurações de informações de dispositivo para extensões de renderização](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
-   O *clientCapabilities* parâmetro que contém uma <xref:System.Collections.Specialized.NameValueCollection> objeto de dicionário que contém informações sobre o cliente para o qual você está renderizando.  
  
-   O *RenderProperties* que contém informações sobre o resultado da renderização.  
  
-   O *createAndRegisterStream* é uma função de delegado a ser chamado para obter um fluxo para renderização.  
  
### <a name="deviceinfo-parameter"></a>Parâmetro deviceInfo  
 O *deviceInfo* parâmetro contém parâmetros de renderização, não os parâmetros de relatório. Esses parâmetros de renderização são passados para a extensão de renderização. O *deviceInfo* valores são convertidos em um <xref:System.Collections.Specialized.NameValueCollection> objeto pelo servidor de relatório. Itens de *deviceInfo* parâmetro são tratados como valores de maiusculas e minúsculas. Se a solicitação de renderização aconteceu como resultado de URL de acesso, os parâmetros de URL na forma `rc:key=value` são convertidos para pares de chave/valor o *deviceInfo* objeto de dicionário. O código de detecção do navegador também fornece os seguintes itens do *clientCapabilities* dicionário: EcmaScriptVersion, JavaScript, MajorVersion, MinorVersion, Win32, tipo e AcceptLanguage. Qualquer par de nome/valor o *deviceInfo* parâmetro não é compreendido pela extensão de renderização será ignorado. O exemplo de código a seguir mostra um método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> de exemplo que recupera ícones:  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>Método RenderStream  
 O método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> processa um fluxo específico do relatório. Todos os fluxos são criados durante a chamada <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> inicial, mas os fluxos não são retornados ao cliente inicialmente. Esse método é usado para fluxos secundários, como imagens em renderização HTML, ou páginas adicionais de uma extensão de renderização de várias páginas, como Imagem/EMF.  
  
## <a name="getrenderingresource-method"></a>Método GetRenderingResource  
 O método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> recupera as informações sem executar toda renderização do relatório. Existem ocasiões em que o relatório necessita de informações que não exigem que o próprio relatório seja renderizado. Por exemplo, se você precisar do ícone associado à extensão de renderização, use o *deviceInfo* parâmetro que contém uma única marca  **\<ícone >**. Nesses casos, você pode usar o método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Visão geral das extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
