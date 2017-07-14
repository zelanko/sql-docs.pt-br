---
title: "Como instalar as extensões de segurança personalizadas | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 58cfeef7d74e0641b965c307551f0fba4a7ff09c
ms.contentlocale: pt-br
ms.lasthandoff: 07/11/2017

---

# Como instalar as extensões de segurança personalizadas
<a id="how-to-install-custom-security-extensions" class="xliff"></a>

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 introduziu um novo portal da web para hospedar novos APIs Odata e também hospedar novas cargas de trabalho de relatório, como KPIS e relatórios móveis. Esse novo portal se baseia em tecnologias mais recentes e é isolado de ReportingServicesService a familiar, executando em um processo separado. Esse processo não é um aplicativo ASP.NET hospedado e como tal quebras suposições de extensões de segurança personalizadas existentes. Além disso, não permite que as interfaces atuais para extensões de segurança personalizadas para qualquer contexto externo ser transmitido, deixando os implementadores com a única opção para inspecionar objetos globais de ASP.NET conhecidos, isso necessário algumas alterações na interface.

## O que mudou?
<a id="what-changed" class="xliff"></a>

Uma nova interface foi introduzida que podem ser implementadas que fornece um IRSRequestContext fornecendo as propriedades mais comuns usadas pelas extensões para tomar decisões relacionadas à autenticação.

Nas versões anteriores, o Gerenciador de relatórios foi front-end e pode ser configurado com sua própria página de logon personalizada. No Reporting Services 2016, apenas uma página hospedada pelo reportserver é suportada e deverá autenticar para ambos os aplicativos.

## Implementação
<a id="implementation" class="xliff"></a>

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

## Implantação e configuração
<a id="deployment-and-configuration" class="xliff"></a>

As configurações básicas necessárias para a extensão de segurança personalizadas são as mesmas que as versões anteriores. As alterações são necessárias para a Web. config e rsreportserver. config: para obter mais informações, consulte [configurar personalizados ou autenticação de formulários no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).

Não é mais um Web. config separado para o Gerenciador de relatórios, o portal herdarão as mesmas configurações que o ponto de extremidade do reportserver.

## Chaves do computador
<a id="machine-keys" class="xliff"></a>

No caso de autenticação de formulários que exige que a descriptografia do cookie de autenticação, os dois processos precisam ser configurados com o mesmo algoritmo de chave e a descriptografia de máquina. Essa era uma etapa familiar para aqueles que anteriormente tinha o programa de instalação do Reporting Services para trabalhar em ambientes de expansão, mas agora é um requisito mesmo para implantações em um único computador.

Você deve usar uma determinada chave de validação para fazer a implantação, há várias ferramentas para gerar as chaves como Gerenciador de serviços de informações para Internet (IIS). Outras ferramentas podem ser encontradas na internet.

### SQL Server Reporting Services 2017 e posterior
<a id="sql-server-reporting-services-2017-and-later" class="xliff"></a>

**\ReportServer\rsReportServer.config**

Adicione `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### SQL Server Reporting Services 2016
<a id="sql-server-reporting-services-2016" class="xliff"></a>

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

### Servidor de Relatório do Power BI
<a id="power-bi-report-server" class="xliff"></a>

Isso está disponível a partir da versão de junho de 2017 (compilação 14.0.600.301).

**\ReportServer\rsReportServer.config**

Adicione `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## Configurar cookies de passagem
<a id="configure-passthrough-cookies" class="xliff"></a>

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

## Próximas etapas
<a id="next-steps" class="xliff"></a>

[Configurar a autenticação de formulários ou personalizado no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurar o Gerenciador de relatórios para transmitir Cookies de autenticação personalizados](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
