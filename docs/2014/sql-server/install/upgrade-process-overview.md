---
title: Visão geral do processo de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb4bfb2073427d0f48b3d4a7ac7b7ab496299030
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091515"
---
# <a name="upgrade-process-overview"></a>Visão geral do processo de atualização
  Este tópico fornece informações sobre as práticas recomendadas do Supervisor de Atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e um resumo dos processos recomendados para a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="upgrade-process"></a>Processo de atualização  
 Os servidores que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] podem ser atualizados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Enquanto alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser atualizados no local, outros precisam ser migrados, e ainda há outros que foram substituídos por novos componentes. Por exemplo, a partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) substitui o DTS (Data Transformation Services), e o DTS não tem mais suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando você formular seu plano de atualização, talvez precise planejar a atualização dos pacotes DTS atuais para pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 O Supervisor de Atualização permite que você avalie as instalações, os componentes e os arquivos relacionados atuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificar problemas conhecidos que causarão problemas durante e após a atualização ou a migração para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Alguns desses problemas conhecidos impedem a atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No relatório do Supervisor de Atualização, esses problemas são identificados como Bloqueadores de Atualização. Se você não resolveu os Bloqueadores de Atualização antes de executar a Instalação, a Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é encerrada e recomenda que você execute o Supervisor de Atualização para identificar os problemas específicos que estão impedindo a atualização.  
  
 Como prática recomendada antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], sugerimos que você faça backup dos dados e das configurações de sistema, e realize etapas estratégicas conforme descrito nas diretrizes operacionais definidas para a sua organização. Use as etapas a seguir para concluir a atualização:  
  
1.  Analise os [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
2.  Faça backup dos dados e configurações do sistema  
  
3.  Execute o Supervisor de Atualização.  
  
     Ele não modifica seus dados ou altera as configurações do seu computador.  
  
4.  Revise os problemas identificados no relatório do Supervisor de Atualização.  
  
5.  Solucione qualquer problema que possa impedir a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  Solucione outros problemas de pré-atualização.  
  
7.  Execute o Supervisor de Atualização para verificar se todos os problemas conhecidos foram solucionados.  
  
8.  Execute a Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
9. Solucione qualquer problema de pós-atualização e de migração.  
  
## <a name="see-also"></a>Consulte também  
 [Executando o Supervisor de atualização &#40;Interface do usuário&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Usando relatórios](../../../2014/sql-server/install/using-reports.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
