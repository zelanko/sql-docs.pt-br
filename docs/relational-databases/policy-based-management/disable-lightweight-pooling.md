---
title: Desabilitar o Lightweight Pooling | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d5bc9651433cc0940732d4818f5d9b8c0f011ad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63008423"
---
# <a name="disable-lightweight-pooling"></a>Desabilitar o Lightweight Pooling
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se o lightweight pooling está desabilitado no servidor. Definir lightweightpooling como 1 faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alterne para a programação de modo fibra. O modo fibra foi projetado para determinadas situações nas quais a alternância de contexto dos trabalhadores UMS é o gargalo importante no desempenho. Como isso é raro, o modo fibra raramente aumenta o desempenho ou a escalabilidade no sistema típico.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 A opção lightweightpooling deve ser habilitada apenas depois de testes extensivos, depois de todas as outras alternativas de ajuste de desempenho serem avaliadas e quando a alternância de contexto for um problema conhecido no seu ambiente.  
  
 Recomendamos que você não use o agendamento do modo fibra para a operação de rotina porque pode diminuir o desempenho ao inibir os benefícios comuns da alternância de contexto e porque alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o TLS (Armazenamento de Thread Local) ou objetos de propriedade de thread, como mutexes (um tipo de objeto kernel de Win32), talvez não funcionem corretamente nesse modo.  
  
 Para remover o lightweight pooling, execute a seguinte instrução e reinicie o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opção lightweight pooling de configuração de Servidor](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
