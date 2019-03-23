---
title: Serviço de acesso para a integração de serviços | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ef77b0dac4db5b30eb12f3a857a3c25cb3caa57
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379514"
---
# <a name="access-to-the-integration-services-service"></a>Acesso ao serviço Integration Services
  Os níveis de proteção do pacote podem limitar quem tem permissão para editar e executar um pacote. É necessário ter proteção adicional para limitar quem pode exibir a lista de pacotes que estão sendo executados em um servidor e quem pode interromper a execução de pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usa o serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para listar os pacotes em execução. Os membros do grupo Administradores do Windows podem visualizar e parar todos os pacotes em execução. Os usuários que não são membros do grupo Administradores podem visualizar e parar apenas os pacotes iniciados por eles.  
  
 É importante restringir o acesso a computadores que executam um serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , especialmente um serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que pode enumerar pastas remotas. Qualquer usuário autenticado pode solicitar a enumeração dos pacotes. Mesmo se o serviço não localizar o serviço, o serviço enumerará as pastas. Esses nomes de pastas podem ser úteis a um usuário mal-intencionados. Se um administrador tiver configurado o serviço para enumerar pastas em uma máquina remota, os usuários também poderão ver os nomes de pastas que eles normalmente não conseguiriam consultar.  
  
  
