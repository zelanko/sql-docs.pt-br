---
title: Domínios do aplicativo e segurança da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34814ab19f96ff7e6232638ef4446b05b5b41ba3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102336"
---
# <a name="application-domains-and-clr-integration-security"></a>Domínios do aplicativo e segurança da integração CLR
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega assemblies que pertencem ao mesmo proprietário no mesmo domínio do aplicativo. Em virtude de um conjunto de assemblies estar sendo executado no mesmo domínio de aplicativo, os assemblies podem descobrir uns aos outros durante a execução usando as interfaces de programação de aplicativo de reflexão do .NET Framework ou outros meios, e podem chamá-los em forma de associação tardia. Pelo fato dessas chamadas estarem ocorrendo nos assemblies que pertencem ao mesmo proprietário, não há permissões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificadas para elas. O esquema de posicionamento de assemblies em domínios de aplicativo é projetado principalmente para obter escalabilidade, segurança e isolamento, podendo ser alterado em versões futuras. Consequentemente, você não deve confiar na localização de assemblies no mesmo domínio do aplicativo através de mecanismos de associação tardia.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
