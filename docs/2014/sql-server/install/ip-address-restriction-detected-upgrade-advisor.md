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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2028e59e91d42bfdced2d18fa6ce129dfb108302
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059242"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Restrição de endereço IP detectada (Supervisor de Atualização)
  O Supervisor de Atualização detectou uma ou mais restrições de endereço IP no site do IIS que hospeda o servidor de relatório ou os diretórios virtuais do Gerenciador de Relatórios. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece suporte nativo para restrições de endereço IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Forma.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A Instalação não pode definir restrições de endereço IP em URLs criadas para um servidor de relatório atualizado. A atualização pode continuar, mas as restrições de endereço IP não serão definidas nas URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Depois da atualização, use o ISA Server, o seu software de firewall ou outra solução para permitir ou excluir solicitações de endereços IP específicos para o servidor de relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
