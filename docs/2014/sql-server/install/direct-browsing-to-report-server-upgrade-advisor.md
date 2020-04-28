---
title: Navegação direta para o servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6945828b2eba829c32d717c13393c9fbda4fc43e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952208"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Navegação Direta para o Servidor de Relatórios (Supervisor de Atualização)
  O supervisor de atualização detectou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que a instalação atual do está navegando diretamente para o diretório virtual do servidor de relatório.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O supervisor de atualização detectou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que a instalação atual do está navegando diretamente para o diretório virtual do servidor de relatório, por exemplo, **http://\<Server Name>/ReportServer**. Isto não tem suporte nas versões atuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Essa regra é um aviso e a atualização não é bloqueada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Navegue usando a interface do usuário do SharePoint para bibliotecas de documentos ou use o **nome do servidor http://\<>/SharePoint site>/_vti_bin/ReportServer**.  
  
  
