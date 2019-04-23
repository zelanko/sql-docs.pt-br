---
title: Funcionalidade descontinuada
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services-2014, sql-server-2014
ms.reviewer: ''
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 3a5472859c582e026fc0c5aafac21abccdc93044
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59949962"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>Funcionalidade descontinuada no SSRS (SQL Server Reporting Services)

  Este tópico descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Não inclui anúncios sobre suporte descontinuado para versões específicas do sistema operacional ou do IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Para obter mais informações sobre os pré-requisitos, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Neste tópico:  
  
- [SQL Server 2014 Reporting Services a funcionalidade descontinuada](#bkmk_sql14)  
  
- [SQL Server 2012 Reporting Services a funcionalidade descontinuada](#bkmk_rc0)  
  
- [SQL Server 2008 R2 Reporting Services a funcionalidade descontinuada](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O Reporting Services descontinuada

 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] O Reporting Services descontinuada

 Esta seção descreve a funcionalidade descontinuada do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services a funcionalidade descontinuada

 Esta seção descreve a funcionalidade descontinuada do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
> Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.
  
### <a name="64-bit-platform-support"></a>Suporte para a plataforma de 64 bits

 A partir do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], o componente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá mais suporte a servidores baseados em Itanium que executam o Windows Server 2003 ou o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a dar suporte a outros sistemas operacionais de 64 bits, incluindo o Windows Server 2008 para sistemas baseados em Itanium e Windows Server 2008 R2 para sistemas baseados em Itanium. Para atualizar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de uma instalação do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em uma edição Itanium-Based System do Windows Server 2003 ou do Windows Server 2003 R2, você deve atualizar o sistema operacional primeiro.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenciais de fonte de dados em acesso a URL

 As cadeias de caracteres de parâmetro de acesso de URL *dsu:datasourcename = value* e *dsp:datasourcename = valor* foram descontinuadas. Em versões anteriores, essas cadeias de caracteres de parâmetros são armazenadas em texto normal no cache do navegador, o que não é seguro.  
  
## <a name="next-steps"></a>Próximas etapas

 - [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [Recursos preteridos do SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)