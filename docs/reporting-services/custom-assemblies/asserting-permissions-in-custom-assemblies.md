---
title: "Declarando permissões em Assemblies personalizados | Microsoft Docs"
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
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 12e12b61a6b2a2a6a58bb88dd3c4f47c2a6eab22
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="asserting-permissions-in-custom-assemblies"></a>Declarando permissões em assemblies personalizados
  Por padrão, o código de assembly personalizado é executado com limitados **execução** conjunto de permissões. Em alguns casos, talvez você queira implementar um assembly personalizado que crie chamadas seguras para proteger recursos em seu sistema de segurança (como um arquivo ou o Registro). Para realizar isso, faça o seguinte:  
  
1.  Identifique as permissões exatas das quais o seu código precisa para fazer a chamada segura. Se esse método é parte de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] biblioteca, essas informações devem ser incluídas na documentação do método.  
  
2.  Modifique os arquivos de configuração de política de servidor de relatório para conceder as permissões exigidas ao assembly personalizado. Para obter mais informações sobre os arquivos de configuração de política de segurança, consulte [usando o Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
3.  Declare as permissões exigidas como parte do método no qual a ligação segura será feita. Isso é necessário porque o código de assembly personalizado que é chamado pelo servidor de relatório é parte do assembly de host do expressão de relatório, que é executado com **execução** permissão por padrão. O **execução** conjunto de permissões permite que o código para ser executado, mas não use recursos protegidos.  
  
4.  Marque o assembly personalizado com **AllowPartiallyTrustedCallersAttribute** se ele está assinado com um nome forte. Isso é necessário porque os assemblies personalizados são chamados de uma expressão de relatório que faz parte do assembly de host do expressão de relatório, que, por padrão, não é concedido **FullTrust**; portanto, é um chamador "parcialmente confiável". Para obter mais informações, consulte [Named Custom Assemblies](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md).  
  
## <a name="implementing-a-secure-call"></a>Implementando uma chamada segura  
 Você pode modificar os arquivos de configuração de política para conceder as permissões específicas ao seu assembly. Por exemplo, se você estiver escrevendo um assembly personalizado para manipular conversão de moedas, talvez seja necessário ler as taxas de câmbio da moeda atual em um arquivo. Para recuperar as informações de taxa, você precisa adicionar uma permissão de segurança adicional, **FileIOPermission**, para o conjunto de permissões para o assembly. Crie a entrada adicional a seguir no arquivo de configuração de política:  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 Em seguida, adicione um grupo de códigos que faça referência ao conjunto de permissões:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 Para que seu código adquira a permissão apropriada, você deve declarar a permissão em seu código de assembly personalizado. Por exemplo, se quiser adicionar acesso somente leitura a um arquivo XML, C:\CurrencyRates.xml, adicione o código a seguir a seu método:  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 Você também pode adicionar a declaraçào como um atributo de método:  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 Para obter mais informações, consulte "Segurança do .NET Framework" no Guia do desenvolvedor do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
