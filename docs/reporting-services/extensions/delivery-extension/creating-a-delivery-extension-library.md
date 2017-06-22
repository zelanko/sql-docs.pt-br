---
title: "Criando uma biblioteca de extensões de entrega | Microsoft Docs"
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
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b893c0702a2a84c1bb354e9bc7859a05e8312ce4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="creating-a-delivery-extension-library"></a>Criando uma biblioteca de extensões de entrega
  Cada extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que você cria deve ser atribuída a um namespace exclusivo e criada em uma biblioteca ou em um arquivo de assembly. O nome exato do namespace não é importante, mas deve ser exclusivo e não deve ser compartilhado com qualquer outra extensão. Você deve criar seus próprios namespaces exclusivos para as extensões de entrega da sua empresa.  
  
 O exemplo a seguir mostra o código para iniciar uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], que usa os namespaces que contêm as interfaces de entrega e qualquer classe utilitária.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 Durante a compilação de uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], forneça ao compilador uma referência a Microsoft.ReportingServices.Interfaces.dll, já que as interfaces e classes de extensão de entrega estão contidas ali. O namespace de <xref:Microsoft.ReportingServices.Interfaces> é necessário para a implementação da interface de <xref:Microsoft.ReportingServices.Interfaces.IExtension>, da interface de <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> e mais. Por exemplo, se todos os arquivos que contém o código para implementar um [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de entrega escrito em c# estivessem em um único diretório com a extensão. cs, o comando a seguir seria emitido a partir desse diretório para compilar os arquivos armazenados em CompanyName.ExtensionName.dll.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 O exemplo de código a seguir mostra o comando que seria usado para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] arquivos com a extensão. vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  Você também pode criar e desenvolver a sua própria extensão de entrega usando o [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Para obter mais informações sobre como desenvolver assemblies no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], consulte a documentação do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
