---
title: Criando uma biblioteca de extensões de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 82f4b71b-dd39-467d-8d8c-6771eb2b12de
caps.latest.revision: 38
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e613df08d9dd50ed769af0138bce8f5373407fc1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116332"
---
# <a name="creating-a-data-processing-extension-library"></a>Criando uma biblioteca de extensões de processamento de dados
  Cada extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que você cria deve ser atribuída a um namespace exclusivo e criada em uma biblioteca ou em um arquivo de assembly. O nome exato do namespace não é importante, mas deve ser exclusivo e não deve ser compartilhado com qualquer outra extensão. O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] usa o namespace <xref:Microsoft.ReportingServices.DataProcessing> para as extensões de processamento de dados fornecidas com o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Crie os seus próprios namespaces exclusivos para as extensões de processamento de dados de sua empresa.  
  
 O exemplo a seguir mostra o código para iniciar uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], que usa os espaços para nome que contêm as interfaces de processamento de dados e qualquer classe utilitária.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.DataProcessing  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.DataProcessing;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 Durante a compilação de uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], forneça ao compilador uma referência a Microsoft.ReportingServices.Interfaces.dll, já que as interfaces de extensão de processamento de dados estão contidas ali. O namespace <xref:Microsoft.ReportingServices.DataProcessing> é necessário para implementar as interfaces de extensão de processamento de dados e o namespace <xref:Microsoft.ReportingServices.Interfaces> é necessário para implementar a interface <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Por exemplo, se todos os arquivos com código para implementar uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] escrita em C# estivessem em um único diretório com a extensão .cs, o comando a seguir seria emitido a partir desse diretório para compilar os arquivos armazenados em CompanyName.ExtensionName.dll.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 O exemplo de código a seguir mostra o comando que será usado para arquivos do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] com a extensão .vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  Você também pode criar, desenvolver e compilar sua própria extensão de processamento de dados usando o [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Para obter mais informações sobre como desenvolver assemblies no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], consulte a documentação do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  