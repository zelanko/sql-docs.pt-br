---
title: "Como instalar as extensões de segurança personalizadas | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e7058e9c0edce2b457dc63bf9e2d5cf61b6ee64f
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="how-to-install-custom-security-extensions"></a>Como instalar as extensões de segurança personalizadas
Reporting Services 2016 introduziu um novo portal da web para hospedar novos APIs Odata e também hospedar novas cargas de trabalho de relatório, como KPIS e relatórios móveis. Esse novo portal se baseia em tecnologias mais recentes e é isolado de ReportingServicesService a familiar, executando em um processo separado. Esse processo não é um aplicativo ASP.NET hospedado e como tal quebras suposições de extensões de segurança personalizadas existentes. Além disso, não permite que as interfaces atuais para extensões de segurança personalizadas para qualquer contexto externo ser transmitido, deixando os implementadores com a única opção para inspecionar objetos globais de ASP.NET conhecidos, isso necessário algumas alterações na interface.

## <a name="what-changed"></a>O que mudou?

Uma nova interface foi introduzida que podem ser implementadas que fornece um IRSRequestContext fornecendo as propriedades mais comuns usadas pelas extensões para tomar decisões relacionadas à autenticação.
    
Nas versões anteriores, o Gerenciador de relatórios foi front-end e pode ser configurado com sua própria página de logon personalizada. No Reporting Services 2016, apenas uma página hospedada pelo reportserver é suportada e deverá autenticar para ambos os aplicativos.

## <a name="implementation"></a>Implementação
Nas versões anteriores, extensões podiam confiar em uma suposição comum que os objetos do ASP.NET seria prontamente disponíveis. Desde que o novo portal não é executado em ASP.NET, a extensão pode pressionar problemas com objetos que são NULL.
    
O exemplo mais genérico está acessando HttpContext para ler as informações de solicitação, como cabeçalhos e cookies. Para permitir extensões tomar decisões mesmo apresentamos um novo método de extensão que fornece informações de solicitação e é chamado durante a autenticação do portal. 
    
As extensões necessárias para implementar o <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> interface para aproveitar isso. As extensões necessárias para implementar as duas versões do <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> método, como é chamado pelo contexto reportserver e outros usado no processo de webhost. O exemplo a seguir mostra uma das implementações simples para o portal em que a identidade resolvida pelo reportserver é usada.

``` 
      public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
      {
           userIdentity = null;
           if (requestContext.User != null)
           {
               userIdentity = requestContext.User;
           }

          // initialize a pointer to the current user id to zero
           userId = IntPtr.Zero;
      }
```

## <a name="deployment-and-configuration"></a>Implantação e configuração
As configurações básicas necessárias para a extensão de segurança personalizadas são as mesmas que as versões anteriores. As alterações são necessárias para a Web. config e rsreportserver. config: para obter mais informações, consulte [configurar personalizados ou autenticação de formulários no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).
    
Não é mais um Web. config separado para o Gerenciador de relatórios, o portal herdarão as mesmas configurações que o ponto de extremidade do reportserver.

## <a name="machine-keys"></a>Chaves do computador

No caso de autenticação de formulários que exige que a descriptografia do cookie de autenticação, os dois processos precisam ser configurados com o mesmo algoritmo de chave e a descriptografia de máquina. Essa era uma etapa familiar para aqueles que anteriormente tinha o programa de instalação do Reporting Services para trabalhar em ambientes de expansão, mas agora é um requisito mesmo para implantações em um único computador.

Por exemplo:
    
**\ReportServer\web.config**

Adicione `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.portal.Webhost.exe.config**

Adicione `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

Você deve usar uma determinada chave de validação para fazer a implantação, há várias ferramentas para gerar as chaves como Gerenciador de serviços de informações para Internet (IIS). Outras ferramentas podem ser encontradas na internet.

## <a name="configure-passthrough-cookies"></a>Configurar cookies de passagem

O novo portal e reportserver se comunicar usando APIs do soap interno para algumas das suas operações (semelhantes para a versão anterior do Gerenciador de relatórios). Quando cookies adicionais devem ser passadas do portal para o servidor as propriedades de PassThroughCookies ainda está disponível. Para obter mais informações, consulte [configurar o Portal da Web para transmitir Cookies de autenticação personalizados](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="see-also"></a>Consulte também

[Configurar a autenticação de formulários ou personalizado no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurar o Gerenciador de relatórios para transmitir Cookies de autenticação personalizados](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)
