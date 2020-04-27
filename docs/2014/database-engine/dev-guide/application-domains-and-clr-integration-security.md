---
title: Domínios de aplicativo e segurança de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f2ff171562929a035cb80fed556c954508c5557
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753768"
---
# <a name="application-domains-and-clr-integration-security"></a>Domínios do aplicativo e segurança da integração CLR
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega assemblies que pertencem ao mesmo proprietário no mesmo domínio do aplicativo. Em virtude de um conjunto de assemblies estar sendo executado no mesmo domínio de aplicativo, os assemblies podem descobrir uns aos outros durante a execução usando as interfaces de programação de aplicativo de reflexão do .NET Framework ou outros meios, e podem chamá-los em forma de associação tardia. Pelo fato dessas chamadas estarem ocorrendo nos assemblies que pertencem ao mesmo proprietário, não há permissões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificadas para elas. O esquema de posicionamento de assemblies em domínios de aplicativo é projetado principalmente para obter escalabilidade, segurança e isolamento, podendo ser alterado em versões futuras. Consequentemente, você não deve confiar na localização de assemblies no mesmo domínio do aplicativo através de mecanismos de associação tardia.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
