---
title: "Gerenciar funções de pacote programaticamente (Serviço SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d8c77d398dbfac21d582b31184e879eb7e2a2d5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Gerenciando funções de pacote programaticamente (Serviço SSIS)
  Ao trabalhar programaticamente com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], talvez você queira determinar quais funções estão disponíveis para aplicar a pacotes ou determinar/definir as funções aplicadas a um único pacote. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.  
  
 As funções se aplicam apenas a pacotes armazenados no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**. Para obter mais informações sobre funções de pacote, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Todos os métodos discutidos neste tópico exigem uma referência ao assembly **Microsoft.SqlServer.ManagedDTS**. Após adicionar a referência em um novo projeto, importe o namespace <xref:Microsoft.SqlServer.Dts.Runtime> usando uma instrução **using** ou **Imports**.  
  
> [!IMPORTANT]  
>  Os métodos da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> para funcionar com o Repositório de Pacotes do SSIS dão suporte apenas a “.”, localhost ou ao nome do servidor local. Você não pode usar "(local)".  
  
## <a name="determining-which-roles-are-available"></a>Determinando quais funções estão disponíveis  
 Para determinar quais funções estão disponíveis para os pacotes armazenados em um servidor específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> da classe <xref:Microsoft.SqlServer.Dts.Runtime.Application>.  
  
## <a name="determining-which-roles-are-assigned"></a>Determinando quais funções são atribuídas  
 Para determinar quais funções já foram atribuídas a um pacote específico, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>. Para atribuir funções a um pacote, chame o método <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Funções do Integration Services &#40;SSIS Service&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
