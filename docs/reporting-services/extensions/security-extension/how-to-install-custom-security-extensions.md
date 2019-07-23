---
title: Como instalar extensões de segurança personalizadas | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fcef802f6c61b85b4905365bda075a9f11d9e10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68223232"
---
# <a name="how-to-install-custom-security-extensions"></a>Como instalar extensões de segurança personalizadas

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

O Reporting Services 2016 introduziu um novo portal da Web para hospedar novas APIs do OData e também hospedar novas cargas de trabalho de relatório, como KPIs e relatórios móveis. Esse novo portal se baseia em tecnologias mais recentes e é isolado do conhecido ReportingServicesService, sendo executado em um processo separado. Esse processo não é um aplicativo ASP.NET hospedado e, como tal, acaba com os pressupostos das extensões de segurança personalizadas existentes. Além disso, as interfaces atuais das extensões de segurança personalizadas não permitem que nenhum contexto externo seja passado, deixando os implementadores com a única opção de inspecionar Objetos ASP.NET globais conhecidos. Isso exigia alterações na interface.

## <a name="what-changed"></a>O que mudou?

Uma nova interface foi introduzida, que pode ser implementada e que fornece um IRSRequestContext, fornecendo as propriedades mais comuns usadas pelas extensões para tomar decisões relacionadas à autenticação.

Nas versões anteriores, o Gerenciador de Relatórios era o front-end e podia ser configurado com sua própria página de logon personalizada. No Reporting Services 2016, há suporte para apenas uma página hospedada pelo reportserver e ela deve se autenticar em ambos os aplicativos.

## <a name="implementation"></a>Implementação

Nas versões anteriores, as extensões podiam confiar em um pressuposto comum de que os objetos ASP.NET estariam prontamente disponíveis. Já que o novo portal não é executado no ASP.NET, a extensão pode ter problemas com objetos sendo NULL.

O exemplo mais genérico é acessar HttpContext.Current para ler as informações de solicitação, como cabeçalhos e cookies. Para permitir que as extensões tomem as mesmas decisões, introduzimos um novo método na extensão que fornece informações de solicitação e é chamado durante a autenticação no portal. 

As extensões devem implementar a interface <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> para aproveitar isso. As extensões precisarão implementar as duas versões do método <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A>, pois ele é chamado pelo contexto do reportserver e o outro é usado no processo do webhost. A amostra abaixo apresenta uma das implementações simples para o portal, em que a identidade resolvida pelo reportserver é a que é usada.

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

As configurações básicas necessárias para a extensão de segurança personalizada são as mesmas das versões anteriores. São necessárias alterações em web.config e rsreportserver.config: para obter mais informações, consulte [Configurar a autenticação personalizada ou de formulários no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).

Não há mais um web.config separado para o Gerenciador de Relatórios; o portal herdará as mesmas configurações do ponto de extremidade do reportserver.

## <a name="machine-keys"></a>Chaves do computador

Para o caso da autenticação de Formulários que exige a descriptografia do cookie de Autenticação, os dois processos precisam ser configurados com a mesma chave do computador e algoritmo de descriptografia. Essa era uma etapa conhecida para aqueles que anteriormente instalavam o Reporting Services para funcionar em ambientes de expansão, mas agora é um requisito até mesmo para implantações em um único computador.

Você deve usar uma chave de validação específica para a implantação; há várias ferramentas para gerar as chaves, como o Gerenciador do IIS (Serviços de Informações da Internet). Outras ferramentas podem ser encontradas na Internet.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 e posterior

**\ReportServer\rsReportServer.config**

Adicione em `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

Adicione em `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

Adicione em `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Servidor de Relatórios do Power BI

Isso está disponível a partir da versão de junho de 2017 (Build 14.0.600.301).

**\ReportServer\rsReportServer.config**

Adicione em `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>Configurar cookies de passagem

O novo portal e o reportserver se comunicam usando APIs SOAP internas para algumas de suas operações (semelhante à versão anterior do Gerenciador de Relatórios). Quando cookies adicionais precisarem ser passados do portal para o servidor, as propriedades de PassThroughCookies ainda estarão disponíveis. Para obter mais informações, consulte [Configurar o portal da Web para passar cookies de autenticação personalizados](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>Próximas etapas

[Configurar autenticação personalizada ou de formulários no servidor de relatório](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurar o Gerenciador de Relatórios para passar cookies de autenticação personalizados](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
