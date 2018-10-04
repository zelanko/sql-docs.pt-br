---
title: Descontinuada no SQL Server Reporting Services no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- discontinued functionality [Reporting Services]
- Reporting Services, backward compatibility
- Rsactivate.exe
- unsupported features [Reporting Services]
ms.assetid: d529cc96-3483-480b-9bfc-bd28b1d0ef52
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ec97f47c87abed0a3fd650632458bf4ba956e985
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100216"
---
# <a name="discontinued-functionality-to-sql-server-reporting-services-in-sql-server-2014"></a>Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Não inclui anúncios sobre suporte descontinuado para versões específicas do sistema operacional ou do IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Para obter mais informações sobre os pré-requisitos, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Neste tópico:  
  
-   [SQL Server 2014 Reporting Services a funcionalidade descontinuada](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services a funcionalidade descontinuada](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services a funcionalidade descontinuada](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O Reporting Services descontinuada  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] O Reporting Services descontinuada  
 Esta seção descreve a funcionalidade descontinuada do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services a funcionalidade descontinuada  
 Esta seção descreve Descontinuado [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="64-bit-platform-support"></a>Suporte para a plataforma de 64 bits  
 A partir [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] componente não oferece suporte a servidores baseados em Itanium que executam o Windows Server 2003 ou Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a dar suporte a outros sistemas operacionais de 64 bits, incluindo o Windows Server 2008 para sistemas baseados em Itanium e Windows Server 2008 R2 para sistemas baseados em Itanium. Para atualizar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de uma instalação do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em uma edição Itanium-Based System do Windows Server 2003 ou do Windows Server 2003 R2, você deve atualizar o sistema operacional primeiro.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenciais de fonte de dados em acesso a URL  
 As cadeias de caracteres de parâmetro de acesso de URL *dsu:datasourcename = value* e *dsp:datasourcename = valor* foram descontinuadas. Em versões anteriores, essas cadeias de caracteres de parâmetros são armazenadas em texto normal no cache do navegador, o que não é seguro.  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Recursos preteridos do SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)  
  
  
