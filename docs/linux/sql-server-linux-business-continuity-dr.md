---
title: "Recuperação de desastres do SQL Server no Linux | Microsoft Docs"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>Recuperação Business continuidade e banco de dados do SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server no Linux permite que as organizações a alcançar uma ampla variedade de metas de contrato de nível de serviço para acomodar vários requisitos de negócios.

As soluções mais simples usam tecnologias de virtualização para atingir um alto grau de resiliência contra falhas de nível de host, a tolerância a falhas contra falhas de hardware, bem como elasticidade e maximização de recursos. Esses sistemas podem executar no local, em uma nuvem privada ou pública ou ambientes híbridos. A forma mais simples de proteção e recuperação de desastres é o backup de banco de dados. Soluções simples disponíveis no SQL Server de 2017 RC2 incluem:

- **Failover VM**
    - Resiliência contra falhas no nível de sistema operacional e de convidado
    - Eventos planejado ou não
    - Tempo de inatividade mínimo para aplicação de patches e atualizações
    - RTO em minutos


- [**Banco de dados de backup e restauração**](sql-server-linux-backup-and-restore-database.md) 
    - Proteção contra corrupção de dados acidental ou maliciosa
    - Proteção de recuperação de desastres
    - RTO em minutos, horas

Técnicas de recuperação de desastres e alta disponibilidade padrão fornecem proteção de nível de instância combinada com uma infraestrutura de armazenamento compartilhado confiável. Para SQL Server 2017 RC2 standard alta disponibilidade inclui:

- [**Cluster de failover**](sql-server-linux-shared-disk-cluster-configure.md)
    - Proteção em nível de instância
    - Failover e a detecção automática de falhas
    - Resiliência contra falhas de sistema operacional e do SQL Server
    - RTO em segundos ou minutos


## <a name="summary"></a>Resumo

SQL Server 2017 RC2 no Linux inclui clusters de failover, backup e restauração e virtualização para dar suporte a alta disponibilidade e recuperação de desastres. 
