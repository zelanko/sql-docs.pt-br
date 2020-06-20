---
title: Recursos das ferramentas de gerenciamento descontinuados no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 724f6e91b911f9edc89188a265364956176d6974
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933127"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>Recursos das Ferramentas de Gerenciamento descontinuados no SQL Server 2014
  Este tópico descreve os recursos das Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="features-removed-in-sscurrent"></a>Recursos removidos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Nenhum  
  
## <a name="features-removed-in-sssql11"></a>Recursos removidos do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 O editor de código do SQL Server Compact Edition foi removido do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. O suporte para o SQL Server Compact Edition também foi removido do Pesquisador de Objetos, Gerenciador de Soluções e Gerenciador de Modelos. Use os editores Transact-SQL no Microsoft Visual Studio 2010 Service Pack 1 ou no Webmatrix.  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>Subsistema de ActiveX para o SQL Server Agent  
 O subsistema de ActiveX para o SQL Server Agent foi removido nesta versão. Não há nenhuma funcionalidade de substituição.  
  
### <a name="sp_addtask-sp_deletetask-sp_updatetask"></a>sp_addtask, sp_deletetask, sp_updatetask  
 Foram removidos Sp_addtask, sp_deletetask e sp_updatetask nesta versão. Não use esta funcionalidade em aplicativos novos ou atualizados.  
  
### <a name="net-send-and-pager-notification"></a>Net Send e notificação de pager  
 Net Send e Notificação de Pager foram removidos nesta versão. Não use esta funcionalidade em aplicativos novos ou atualizados.  
  
### <a name="data-tier-applications"></a>Aplicativos da camada de Dados  
 Alguns recursos de DAC (aplicativo da camada de dados) presentes no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] foram removidos no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. No entanto, a Estrutura de Aplicativo da Camada de Dados (DACfx versão 3.0) lançada com o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] é compatível com o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] até o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e o [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. O DAC versão 3.0 não tem suporte de versões antigas do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , incluindo o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]. Os projetos de bancos de dados do Visual Studio 2010 não dão suporte a pacotes DACPAC do DAC 3.0 ou pacotes de exportação DAC (BACPAC) gerados com o DACfx versão 3.0 ou posterior.  
  
 A Microsoft recomenda usar a versão mais recente disponível dos projetos de banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
 A API do DACfx 3.0 e as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferecem suporte à leitura de arquivos DACPAC e BACPAC criados usando ferramentas anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e versões do DACfx: extraindo bancos de dados em arquivos DACPAC dessas versões e implantando bancos de dados em versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com suporte por meio do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
## <a name="see-also"></a>Consulte Também  
 [Compatibilidade com versões anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
