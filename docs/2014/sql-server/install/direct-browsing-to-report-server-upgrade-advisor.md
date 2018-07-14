---
title: Navegação direta para o servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 482fc74e08a60ed7f4d81a450a680c43a9815d5a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196676"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Navegação Direta para o Servidor de Relatórios (Supervisor de Atualização)
  O Supervisor de atualização detectou que sua instalação atual do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está navegando diretamente para o diretório virtual do servidor de relatório.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 O Supervisor de atualização detectou que sua instalação atual do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está navegando diretamente para o diretório virtual do servidor de relatório, por exemplo **http://\<nome do servidor > / ReportServer**. Isto não tem suporte nas versões atuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Essa regra é um aviso e a atualização não é bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Navegar usando a interface de usuário do SharePoint para bibliotecas de documentos ou usar **http://\<nome do servidor > / site do sharepoint vti_bin/reportserver**.  
  
  
