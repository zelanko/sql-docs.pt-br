---
title: Os diretórios virtuais não estão especificados (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 79ab9c0d18f20bcfd6f549918cc1501a1d8e1e49
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065107"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>Diretórios virtuais não especificados (Supervisor de Atualização)
  O Supervisor de Atualização não detectou configurações de diretório virtual para o serviço Web Servidor de Relatórios ou para o Gerenciador de Relatórios. Concluída a atualização, configure as reservas de URL do servidor de relatório usando o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A atualização de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui a reserva de novas URLs para o serviço Web Servidor de Relatórios e para o Gerenciador de Relatórios. O Supervisor de Atualização não detectou diretórios virtuais para o servidor de relatório ou para o Gerenciador de Relatórios da instância que será atualizada, sendo assim, o processo de atualização possui informações insuficientes para a criação de reservas de URL para o servidor de relatório atualizado. A atualização pode prosseguir, mas o servidor de relatório ou o diretório virtual do Gerenciador de Relatórios ficará indefinido após a atualização da instalação.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Concluída a atualização, use o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir as URLs do servidor de relatório e do Gerenciador de Relatórios. Use o Gerenciador do IIS para remover todos os diretórios virtuais que não serão mais necessários.  
  
 Para obter mais informações, consulte [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
