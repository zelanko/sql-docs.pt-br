---
description: Verificar a configuração máxima de threads de trabalho
title: Verificar a configuração máxima de threads de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8c82c2359a8dd4828b8d7da465752eeec44c70f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420470"
---
# <a name="verify-max-worker-threads-setting"></a>Verificar a configuração máxima de threads de trabalho
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica a opção do servidor de máximo de threads de trabalho para configurações potencialmente incorretas. A configuração da opção de máximo de threads de trabalho com um valor pequeno pode impedir que threads suficientes atendam às solicitações de entrada do cliente de maneira oportuna e, assim, causar uma "escassez de threads". Entretanto, a configuração da opção com um valor grande pode desperdiçar espaço de endereço, porque cada thread ativo consome até 4 KB em servidores de 64 bits.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção max worker threads como 0. Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automaticamente o número correto de threads de trabalho ativos com base nas solicitações do usuário.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Configurar a opção max worker threads de configuração de servidor](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
