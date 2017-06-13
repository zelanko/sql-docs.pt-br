---
title: "Considerações de segurança para extensões | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
caps.latest.revision: 30
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c7e953f9beea75f08e6c87a210975172e5768d68
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="security-considerations-for-extensions"></a>Considerações de segurança para extensões
  Todos aplicativo que se destinam ao CLR (Common Language Runtime) devem interagir com o sistema de segurança CLR. Quando tal aplicativo é executado, é automaticamente avaliado e recebe um conjunto de permissões do CLR. Dependendo das permissões que o aplicativo receber, ele continuará sua execução ou vai gerar uma exceção de segurança. As configurações e as diretrizes locais de segurança dos arquivos de configuração de política de segurança para um determinado servidor de relatório definem as permissões de código recebidas por um assembly.  
  
 Antes de solicitar permissões, você precisa estar ciente dos recursos e das operações protegidas que o seu código de extensão planeja usar, além de saber que permissões protegem esses recursos e operações. Além disso, você precisa manter o controle sobre qualquer recurso acessado por qualquer método de biblioteca de classes chamado pelos componentes de extensão. Para obter mais informações, consulte "Solicitando permissões" no Guia do desenvolvedor do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 As extensões implantadas em um servidor de relatório devem ser executado como totalmente confiável, que significa que sua extensão precisa fazer parte de um grupo de código que recebe o **FullTrust** conjunto de permissões. Isso também significa que a sua extensão poderá ter acesso a certos recursos e operações de servidor disponíveis por meio do CLR, dependendo do usuário autenticado para um determinado relatório. Para obter mais informações sobre grupos de código e extensões, consulte [Code Access Security no Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md).  
  
> [!IMPORTANT]  
> O  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impõe a segurança [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para todas as suas extensões.  
  
 As condições a seguir se aplicam à implantação de processamento de dados, à entrega, à renderização e às extensões de segurança do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   Somente o administrador local tem permissão para implantar uma extensão.  
  
-   Somente os usuários com as permissões de leitura/gravação apropriadas podem alterar os arquivos de configuração para o componente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está sendo estendido.  
  
-   Somente os usuários privilegiados têm permissão para editar os arquivos de política de segurança e para habilitar a segurança de acesso a código para uma extensão.  
  
 Para obter mais informações sobre a segurança de acesso do código em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [desenvolvimento seguro &#40; Reporting Services &#41; ](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
 Para obter mais informações sobre segurança [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte "Segurança do .NET Framework" no seu Guia do desenvolvedor do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="initialization-of-extension-assemblies"></a>Inicialização de assemblies de extensão  
 Quando as extensões são carregadas na memória pela primeira vez pelo servidor de relatório, usam as credenciais da conta de serviço, já que alguns assemblies de extensão exigem permissões específicas para o acesso a recursos do sistema, para ler arquivos de configuração e para carregar outros assemblies dependentes. Após o carregamento de um assembly e de sua inicialização, no entanto, todas as chamadas subsequentes a assemblies de extensão usarão as credenciais da conta do usuário conectado no momento.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
