---
title: O tamanho do pacote de rede não deve exceder 8060 Bytes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3652e83a63a088d2af0e26c401d30484df5c76b0
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811402"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>O tamanho do pacote de rede não dever exceder 8060 bytes
  Se o valor especificado para sp_configure 'network packet size' ou se o tamanho do pacote de rede de qualquer usuário que fez logon for maior que 8060, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará operações de alocação de memória diferentes. Isso pode causar um aumento no espaço de endereço virtual de processo que não está reservado para o pool de buffers.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 O tamanho do pacote de rede não dever exceder 8060 bytes  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Artigo 903002 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
