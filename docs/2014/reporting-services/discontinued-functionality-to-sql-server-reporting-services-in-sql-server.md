---
title: Funcionalidade do SQL Server Reporting Services no SQL Server 2014 descontinuada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- discontinued functionality [Reporting Services]
- Reporting Services, backward compatibility
- Rsactivate.exe
- unsupported features [Reporting Services]
ms.assetid: d529cc96-3483-480b-9bfc-bd28b1d0ef52
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 627e8fe70de053c0cd53cc24c77438549c794e76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115377"
---
# <a name="discontinued-functionality-to-sql-server-reporting-services-in-sql-server-2014"></a>Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Não inclui anúncios sobre suporte descontinuado para versões específicas do sistema operacional ou do IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Para obter mais informações sobre os pré-requisitos do sistema, consulte [requisitos de Hardware e Software para instalar o SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Neste tópico:  
  
-   [Funcionalidade descontinuada SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
-   [Funcionalidade descontinuada SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Funcionalidade descontinuada SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O Reporting Services funcionalidade descontinuada  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] O Reporting Services funcionalidade descontinuada  
 Esta seção descreve a funcionalidade descontinuada do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_kj"></a> Funcionalidade descontinuada SQL Server 2008 R2 Reporting Services  
 Esta seção descreve Descontinuado [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="64-bit-platform-support"></a>Suporte para a plataforma de 64 bits  
 A partir do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] componente não oferece suporte a servidores baseados em Itanium que executam o Windows Server 2003 ou Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a dar suporte a outros sistemas operacionais de 64 bits, incluindo o Windows Server 2008 para sistemas baseados no Itanium e Windows Server 2008 R2 para sistemas baseados em Itanium. Para atualizar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de uma instalação do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em uma edição Itanium-Based System do Windows Server 2003 ou do Windows Server 2003 R2, você deve atualizar o sistema operacional primeiro.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenciais de fonte de dados em acesso a URL  
 As cadeias de caracteres de parâmetro de acesso de URL *dsu:datasourcename = valor* e *dsp:datasourcename = valor* foram descontinuadas. Em versões anteriores, essas cadeias de caracteres de parâmetros são armazenadas em texto normal no cache do navegador, o que não é seguro.  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Alterações de comportamento no SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Recursos preteridos do SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)  
  
  