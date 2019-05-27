---
title: Restrição de endereço IP detectada (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ec72f58aaa0a10d0fa13860bc39e81b717d0ff89
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094174"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Restrição de endereço IP detectada (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma ou mais restrições de endereço IP no site do IIS que hospeda o servidor de relatório ou os diretórios virtuais do Gerenciador de Relatórios. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece suporte nativo para restrições de endereço IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A Instalação não pode definir restrições de endereço IP em URLs criadas para um servidor de relatório atualizado. A atualização pode continuar, mas as restrições de endereço IP não serão definidas nas URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Depois da atualização, use o ISA Server, o seu software de firewall ou outra solução para permitir ou excluir solicitações de endereços IP específicos para o servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
