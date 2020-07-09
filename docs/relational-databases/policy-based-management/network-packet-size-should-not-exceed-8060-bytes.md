---
title: O tamanho do pacote de rede não deve exceder 8060 Bytes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7800bf2c9724cec7ba8100e7268e1760e39d3afe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785067"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>O tamanho do pacote de rede não dever exceder 8060 bytes
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se o valor especificado para sp_configure 'network packet size' ou se o tamanho do pacote de rede de qualquer usuário que fez logon for maior que 8060, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará operações de alocação de memória diferentes. Isso pode causar um aumento no espaço de endereço virtual de processo que não está reservado para o pool de buffers.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 O tamanho do pacote de rede não dever exceder 8060 bytes  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Artigo 903002 da Base de Dados de Conhecimento Microsoft](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
