---
title: Visão geral de segurança (Replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- authorization [SQL Server replication]
- cryptography [SQL Server replication]
- encryption [SQL Server replication]
- security [SQL Server replication], about security
- authentication [SQL Server replication]
ms.assetid: 27828fe4-3b54-4c33-886e-08e8279e34b5
caps.latest.revision: 44
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a3ca129d5dd03d788f639a51322ceb999a25e76a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008616"
---
# <a name="security-overview-replication"></a>Visão geral de segurança (Replicação)
  Essencialmente, como ajudar a proteger seu ambiente de replicação é uma questão de compreender as opções de autorização e autenticação, compreender o uso apropriado dos recursos de filtragem de replicação e aprender medidas específicas de como ajudar a proteger cada parte do ambiente de replicação. O ambiente de replicação inclui o Distribuidor, o Publicador, os Assinantes e a pasta de instantâneos. Este capítulo aborda a segurança de replicação, mas a segurança de replicação é criada na segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e segurança do Windows. Portanto, você deve compreender esta base e as particularidades da segurança de replicação. Para obter mais informações, consulte [Considerações de segurança para uma instalação do SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md). Para obter mais informações sobre considerações de segurança para publicações Oracle, consulte a seção "Modelo de segurança de replicação" no tópico [Design Considerations and Limitations for Oracle Publishers](../non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Ameaça e mitigação de vulnerabilidade &#40;Replicação&#41;](threat-and-vulnerability-mitigation-replication.md)  
 Discute ameaças potenciais a uma topologia de replicação e descreve maneiras para reduzir essas ameaças.  
  
 [Identidade e controle de acesso &#40;Replicação&#41;](identity-and-access-control-replication.md)  
 Descreve como usar autenticação, autorização e filtragem para ajudar a proteger uma topologia de replicação.  
  
 [Desenvolvimento seguro &#40;Replicação&#41;](secure-development-replication.md)  
 Descreve o comportamento de segurança de replicação, práticas recomendadas de segurança de replicação e menos permissões para replicação.  
  
 [Implantação segura &#40;Replicação&#41;](secure-deployment-replication.md)  
 Descreve como proteger melhor todos os componentes de uma topologia de replicação  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e proteção &#40;Replicação&#41;](security-and-protection-replication.md)  
  
  