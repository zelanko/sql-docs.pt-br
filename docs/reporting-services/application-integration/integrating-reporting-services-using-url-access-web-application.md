---
title: Usando o acesso à URL em um aplicativo Web | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bf79a9f1c6790abfb1a2435e533aa0847abbd3b6
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813979"
---
# <a name="integrating-reporting-services-using-url-access---web-application"></a>Integrando o Reporting Services usando o acesso à URL – aplicativo Web
  O acesso à URL no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi especificamente criado para permitir o acesso a relatórios individuais pela rede. Esse tipo de acesso é melhor para a integração da exibição de relatórios e da navegação em um aplicativo Web personalizado. Para usar o acesso à URL em aplicativos Web, você pode:  
  
-   Envie uma URL a um servidor de relatório específico a partir de um site ou de portal.  
  
-   Use um método POST e passe parâmetros de cadeia de caracteres da consulta para uma URL do servidor de relatório usando campos de formulário.  
  
## <a name="url-access-through-direct-addressing"></a>Acesso à URL por meio de endereçamento direto  
 Para acessar um servidor de relatório ou item de banco de dados do servidor de relatório usando uma URL, basta fornecer o endereço da URL em um navegador da Web ou aplicativo. Você também pode fornecer parâmetros à URL que podem afetar a aparência do relatório ou do recurso acessado. Uma URL pode ter como destino um servidor de relatório por meio da barra de endereços de um navegador da Web ou uma URL pode ser a origem de um **IFrame** que faz parte de um aplicativo Web maior ou de um portal. Você pode incluir hiperlinks para relatórios em várias páginas da Web do seu portal, além de ter como destino um quadro específico para o relatório ou abrir uma nova janela do navegador no processo.  
  
 No exemplo a seguir, o hiperlink tem como destino um quadro chamado "main", que poderia ser diferente do que inclui o hiperlink. O hiperlink poderia fazer parte de um portal da Web.  
  
```  
<a href="https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 No exemplo anterior, a configuração de informações de dispositivo **LinkTarget** é passada com um valor “main” na cadeia de consulta da URL. Isso garante que qualquer hiperlink de detalhamento do relatório também terá como destino o quadro chamado "main".  
  
 Para obter mais informações sobre as configurações de informações de dispositivo, consulte [Passando as configurações de informações de dispositivo para extensões de renderização](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Observe que muitos servidores e navegadores limitam o número de caracteres permitidos em uma URL. Em alguns casos, é imposto um limite de 256 caracteres. Para contornar essa limitação, você poderá usar solicitações POST usando submissão de formulário.  
  
> [!NOTE]  
>  O Internet Explorer tem um comprimento máximo de URL de 2.083 caracteres. Esse limite se aplica às URLs de solicitação POST e GET. No entanto, POST não está limitado pelo tamanho da URL para o envio de pares de nome/valor como parte de um formulário, já que eles são transferidos no cabeçalho e não na URL.  
  
## <a name="url-access-through-a-form-post-method"></a>Acesso à URL por meio de um método POST de formulário  
 Quando um usuário solicita dados de um servidor de relatório usando acesso à URL, a solicitação HTTP usa o método GET. Isso é equivalente a uma submissão de formulário onde METHOD= "GET". Solicitações de URL ou submissões de formulário que usam METHOD= "GET" estão limitados pelo número máximo de caracteres que um servidor ou navegador da Web pode processar.  
  
 Com as solicitações POST (METHOD= "POST" e campos de entrada), os pares de nome/valor são transferidos no cabeçalho e não na URL. Dessa forma, os pares de nome/valor da cadeia de caracteres de consulta não fazem parte da URL, permitindo que você forneça listas de parâmetros mais longas e mais complexas.  
  
 Usando o acesso direto, um usuário pode ver a URL para o servidor de relatório e poderá ser capaz de modificar a cadeia de caracteres de consulta ou observar os parâmetros de solicitação URL e do servidor de relatório para uso posterior.  
  
 O HTML de exemplo a seguir demonstra a utilização de um formulário que pode ser usado para ter como destino um servidor de relatório com uma URL específica e passar parâmetros de cadeia de caracteres de consulta como parte dos campos de entrada do formulário.  
  
```  
<FORM id="frmRender" action="https://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 No exemplo anterior, se um usuário clicar no botão do formulário, o servidor de relatório retornará um relatório renderizado em HTML destinado ao quadro atual. Uma cadeia de caracteres de acesso à URL comparável poderia ficar assim:  
  
```  
https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrando o Reporting Services usando o acesso à URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Usando o acesso à URL em um aplicativo do Windows](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [Acesso à URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)  
  
  
