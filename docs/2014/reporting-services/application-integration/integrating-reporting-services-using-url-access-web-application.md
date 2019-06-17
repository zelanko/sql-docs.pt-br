---
title: Usando o acesso à URL em um aplicativo Web | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6a8625af05b13331d513608bc20eb8dd9678d01a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714573"
---
# <a name="using-url-access-in-a-web-application"></a>Usando o acesso à URL em um aplicativo Web
  O acesso à URL no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi especificamente criado para permitir o acesso a relatórios individuais pela rede. Esse tipo de acesso é melhor para a integração da exibição de relatórios e da navegação em um aplicativo Web personalizado. Para usar o acesso à URL em aplicativos Web, você pode:  
  
-   Envie uma URL a um servidor de relatório específico a partir de um site ou de portal.  
  
-   Use um método POST e passe parâmetros de cadeia de caracteres da consulta para uma URL do servidor de relatório usando campos de formulário.  
  
## <a name="url-access-through-direct-addressing"></a>Acesso à URL por meio de endereçamento direto  
 Para acessar um servidor de relatório ou item de banco de dados do servidor de relatório usando uma URL, basta fornecer o endereço da URL em um navegador da Web ou aplicativo. Você também pode fornecer parâmetros à URL que podem afetar a aparência do relatório ou do recurso acessado. Uma URL pode ter como destino um servidor de relatório por meio da barra de endereços de um navegador da Web ou uma URL pode ser a origem de um **IFrame** que faz parte de um aplicativo Web maior ou de um portal. Você pode incluir hiperlinks para relatórios em várias páginas da Web do seu portal, além de ter como destino um quadro específico para o relatório ou abrir uma nova janela do navegador no processo.  
  
 No exemplo a seguir, o hiperlink tem como destino um quadro chamado "main", que poderia ser diferente do que inclui o hiperlink. O hiperlink poderia fazer parte de um portal da Web.  
  
```  
<a href="http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 No exemplo anterior, a configuração de informações de dispositivo **LinkTarget** é passada com um valor “main” na cadeia de consulta da URL. Isso garante que qualquer hiperlink de detalhamento do relatório também terá como destino o quadro chamado "main".  
  
 Para obter mais informações sobre as configurações de informações de dispositivo, consulte [Passando as configurações de informações de dispositivo para extensões de renderização](../report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Observe que muitos servidores e navegadores limitam o número de caracteres permitidos em uma URL. Em alguns casos, é imposto um limite de 256 caracteres. Para contornar essa limitação, você poderá usar solicitações POST usando submissão de formulário.  
  
> [!NOTE]  
>  O Internet Explorer tem um comprimento máximo de URL de 2.083 caracteres. Esse limite se aplica às URLs de solicitação POST e GET. No entanto, POST não está limitado pelo tamanho da URL para o envio de pares de nome/valor como parte de um formulário, já que eles são transferidos no cabeçalho e não na URL.  
  
## <a name="url-access-through-a-form-post-method"></a>Acesso à URL por meio de um método POST de formulário  
 Quando um usuário solicita dados de um servidor de relatório usando acesso à URL, a solicitação HTTP usa o método GET. Isso é equivalente a uma submissão de formulário onde METHOD= "GET". Solicitações de URL ou submissões de formulário que usam METHOD= "GET" estão limitados pelo número máximo de caracteres que um servidor ou navegador da Web pode processar.  
  
 Com as solicitações POST (METHOD= "POST" e campos de entrada), os pares de nome/valor são transferidos no cabeçalho e não na URL. Dessa forma, os pares de nome/valor da cadeia de caracteres de consulta não fazem parte da URL, permitindo que você forneça listas de parâmetros mais longas e mais complexas.  
  
 Usando o acesso direto, um usuário pode ver a URL para o servidor de relatório e poderá ser capaz de modificar a cadeia de caracteres de consulta ou observar os parâmetros de solicitação URL e do servidor de relatório para uso posterior.  
  
 O HTML de exemplo a seguir demonstra a utilização de um formulário que pode ser usado para ter como destino um servidor de relatório com uma URL específica e passar parâmetros de cadeia de caracteres de consulta como parte dos campos de entrada do formulário.  
  
```  
<FORM id="frmRender" action="http://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 No exemplo anterior, se um usuário clicar no botão do formulário, o servidor de relatório retornará um relatório renderizado em HTML destinado ao quadro atual. Uma cadeia de caracteres de acesso à URL comparável poderia ficar assim:  
  
```  
http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>Consulte também  
 [Integrando o Reporting Services em aplicativos](../application-integration/integrating-reporting-services-into-applications.md)   
 [Integrando o Reporting Services usando o acesso à URL](integrating-reporting-services-using-url-access.md)   
 [Usando o acesso à URL em um aplicativo do Windows](integrating-reporting-services-using-url-access-windows-application.md)   
 [Acesso à URL &#40;SSRS&#41;](../url-access-ssrs.md)  
  
  
