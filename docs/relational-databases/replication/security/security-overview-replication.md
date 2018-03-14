---
title: "Visão geral de segurança (Replicação) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authorization [SQL Server replication]
- cryptography [SQL Server replication]
- encryption [SQL Server replication]
- security [SQL Server replication], about security
- authentication [SQL Server replication]
ms.assetid: 27828fe4-3b54-4c33-886e-08e8279e34b5
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6aeaff943dfd5a20c7e8cd68424a0294b7e694b7
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="security-overview-replication"></a>Visão geral de segurança (Replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Essencialmente, como ajudar a proteger seu ambiente de replicação é uma questão de compreender as opções de autorização e autenticação, compreender o uso apropriado dos recursos de filtragem de replicação e aprender medidas específicas de como ajudar a proteger cada parte do ambiente de replicação. O ambiente de replicação inclui o Distribuidor, o Publicador, os Assinantes e a pasta de instantâneos. Este capítulo aborda a segurança de replicação, mas a segurança de replicação é criada na segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e segurança do Windows. Portanto, você deve compreender esta base e as particularidades da segurança de replicação. Para obter mais informações, consulte [Considerações de segurança para uma instalação do SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md). Para obter mais informações sobre considerações de segurança para publicações Oracle, consulte a seção "Modelo de segurança de replicação" no tópico [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Ameaça e mitigação de vulnerabilidade &#40;Replicação&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
 Discute ameaças potenciais a uma topologia de replicação e descreve maneiras para reduzir essas ameaças.  
  
 [Identidade e controle de acesso &#40;Replicação&#41;](../../../relational-databases/replication/security/identity-and-access-control-replication.md)  
 Descreve como usar autenticação, autorização e filtragem para ajudar a proteger uma topologia de replicação.  
  
 [Desenvolvimento seguro &#40;Replicação&#41;](../../../relational-databases/replication/security/secure-development-replication.md)  
 Descreve o comportamento de segurança de replicação, práticas recomendadas de segurança de replicação e menos permissões para replicação.  
  
 [Implantação segura &#40;Replicação&#41;](../../../relational-databases/replication/security/secure-deployment-replication.md)  
 Descreve como proteger melhor todos os componentes de uma topologia de replicação  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
