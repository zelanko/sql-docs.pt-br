---
title: O tamanho do pacote de rede não deve exceder 8060 Bytes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d66ba3298b2346e2ec139f27ec53d6104ad0ac9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625804"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>O tamanho do pacote de rede não dever exceder 8060 bytes
  Se o valor especificado para sp_configure 'network packet size' ou se o tamanho do pacote de rede de qualquer usuário que fez logon for maior que 8060, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará operações de alocação de memória diferentes. Isso pode causar um aumento no espaço de endereço virtual de processo que não está reservado para o pool de buffers.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 O tamanho do pacote de rede não dever exceder 8060 bytes  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Artigo 903002 da Base de Dados de Conhecimento Microsoft](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
