---
title: Forçar serviço de espelhamento de banco de dados
description: Se o servidor principal falhar enquanto o servidor espelho estiver disponível, torne o banco de dados disponível forçando o failover do serviço para o banco de dados espelhado (com possível perda de dados)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- forced service [SQL Server]
- database mirroring [SQL Server], forcing service
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 970f399ab6227fdaf2672bf887c250b6be02de1e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74822223"
---
# <a name="force-service-in-a-database-mirroring-session-transact-sql"></a>Forçar serviço em uma sessão de espelhamento de banco de dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Em modo de alto desempenho e em modo de alta segurança sem failover automático, se o servidor principal falhar enquanto o servidor espelho estiver disponível, o proprietário do banco de dados poderá disponibilizar o banco de dados forçando o serviço para failover (com possível perda de dados) no banco de dados espelho. Essa opção só está disponível sob todas as condições seguintes:  
  
-   O servidor principal está fora de operação.  
  
-   WITNESS está definido como OFF ou está conectado ao servidor espelho.  
  
> [!CAUTION]  
>  O serviço forçado é estritamente um método de recuperação de desastre. O serviço forçado pode envolver alguma perda de dados. Portanto, só force o serviço se você estiver disposto a se arriscar perder alguns dados para restaurar o serviço no banco de dados imediatamente. Se forçar o serviço resultar em perda significativa de dados, recomendamos que você pare o espelhamento e sincronize novamente os bancos de dados manualmente. Para obter mais informações sobre os riscos de forçar o serviço, veja [Modos de operação do espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 Quando o serviço é forçado, a sessão é suspensa e um novo ponto de bifurcação da recuperação é iniciado. O efeito de forçar o serviço é semelhante a remover o espelhamento e recuperar o banco de dados principal antigo. No entanto, forçar o serviço facilita nova sincronização dos bancos de dados (com possível perda de dados) quando o espelhamento é retomado.  
  
### <a name="to-force-service-in-a-database-mirroring-session"></a>Para forçar serviço em uma sessão de espelhamento de banco de dados  
  
1.  Conecte-se ao servidor espelho.  
  
2.  Emita a seguinte instrução:  
  
     ALTER DATABASE *<nome_banco_dados>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     em que *<nome_banco_dados>* é o banco de dados espelhado.  
  
     O servidor espelho imediatamente faz a transição para servidor principal e o espelhamento é suspenso.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Modos de operação de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
