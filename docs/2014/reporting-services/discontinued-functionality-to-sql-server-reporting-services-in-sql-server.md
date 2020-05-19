---
title: Funcionalidade descontinuada
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8cdec8ed3fbdd539b0c630af2a298ebf9807d6a7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755760"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>Funcionalidade descontinuada no SSRS (SQL Server Reporting Services)

  Este tópico descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Não inclui anúncios sobre suporte descontinuado para versões específicas do sistema operacional ou do IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../includes/msconame-md.md)] . Para obter mais informações sobre os pré-requisitos do sistema, consulte [requisitos de hardware e software para a instalação do SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Neste tópico:  
  
- [SQL Server 2014 Reporting Services funcionalidade descontinuada](#bkmk_sql14)  
  
- [Funcionalidade descontinuada do SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
- [Funcionalidade descontinuada do SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-discontinued-functionality"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Reporting Services funcionalidade descontinuada

 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="sssql11-reporting-services-discontinued-functionality"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Reporting Services funcionalidade descontinuada

 Esta seção descreve a funcionalidade descontinuada do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi descontinuado no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="sql-server-2008-r2-reporting-services-discontinued-functionality"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services funcionalidade descontinuada

 Esta seção descreve o descontinuado no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
> Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.
  
### <a name="64-bit-platform-support"></a>Suporte para a plataforma de 64 bits

 A partir do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], o componente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não dá mais suporte a servidores baseados em Itanium que executam o Windows Server 2003 ou o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]O  continua dar suporte a outros sistemas operacionais de 64 bits. incluindo o Windows Server 2008 for Itanium-Based Systems e o Windows Server°2008°R2 for Itanium-Based Systems. Para atualizar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de uma instalação do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em uma edição Itanium-Based System do Windows Server 2003 ou do Windows Server 2003 R2, você deve atualizar o sistema operacional primeiro.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenciais de fonte de dados em acesso a URL

 As cadeias de caracteres de parâmetro de acesso à URL *DSU: DataSourceName = Value* e *DSP: DataSourceName = Value* agora são descontinuadas. Em versões anteriores, essas cadeias de caracteres de parâmetros são armazenadas em texto normal no cache do navegador, o que não é seguro.  
  
## <a name="next-steps"></a>Próximas etapas

 - [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [Recursos preteridos do SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)