---
title: "Gerenciando funções de pacote programaticamente (serviço SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Gerenciando funções de pacote programaticamente (Serviço SSIS)
  Ao trabalhar programaticamente com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], talvez você queira determinar quais funções estão disponíveis para aplicar a pacotes ou determinar/definir as funções aplicadas a um único pacote. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.  
  
 Funções se aplicam apenas a pacotes armazenados na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** banco de dados. Para obter mais informações sobre as funções do pacote, consulte [funções do Integration Services &#40; Serviço do SSIS &#41; ](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos os métodos discutidos neste tópico exigem uma referência para o **manageddts** assembly. Após adicionar a referência em um novo projeto, importe o <xref:Microsoft.SqlServer.Dts.Runtime> namespace usando um **usando** ou **Imports** instrução.  
  
> [!IMPORTANT]  
>  Os métodos do <xref:Microsoft.SqlServer.Dts.Runtime.Application> suporta somente a classe para trabalhar com o repositório de pacotes do SSIS ".", localhost ou o nome do servidor para o servidor local. Você não pode usar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinando quais funções estão disponíveis  
 Para determinar quais funções estão disponíveis para os pacotes armazenados em um servidor específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinando quais funções são atribuídas  
 Para determinar quais funções já foram atribuídas a um pacote específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para atribuir funções a um pacote, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40; do Integration Services Serviço do SSIS &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
