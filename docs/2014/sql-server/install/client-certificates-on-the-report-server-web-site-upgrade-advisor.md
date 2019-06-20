---
title: Certificados de cliente no site da web de servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a0a8fb06eabb6fa07e503c00d3651020d52cff26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096482"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>Certificados cliente no site do servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou um ou mais certificados de cliente no site do IIS que hospeda o servidor de relatório ou os diretórios virtuais do Gerenciador de Relatórios.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não oferece suporte ao uso de certificados de cliente para autenticar usuários. A atualização pode continuar, mas os certificados de cliente não serão usados pelo servidor de relatório atualizado.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Será necessário usar outra solução, como o ISA Server, para garantir que quaisquer requisitos de autenticação de certificado de cliente sejam atendidos.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
