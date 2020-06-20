---
title: Verificar a configuração máxima de threads de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5dbffb87f58d2beb633f43ff18680222ea62cf5e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047737"
---
# <a name="verify-max-worker-threads-setting"></a>Verificar a configuração máxima de threads de trabalho
  Esta regra verifica a opção do servidor de máximo de threads de trabalho para configurações potencialmente incorretas. A configuração da opção de máximo de threads de trabalho com um valor pequeno pode impedir que threads suficientes atendam às solicitações de entrada do cliente de maneira oportuna e, assim, causar uma "escassez de threads". Entretanto, a configuração da opção com um valor grande pode desperdiçar espaço de endereço, porque cada thread ativo consome 512 KB de servidores de 32 bits e até 4 MB de servidores de 64 bits.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção max worker threads como 0. Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automaticamente o número correto de threads de trabalho ativos com base nas solicitações do usuário.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Configurar a opção max worker threads de configuração de servidor](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
