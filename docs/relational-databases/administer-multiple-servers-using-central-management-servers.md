---
title: "Administrar vários servidores usando os Servidores Centrais de Gerenciamento | Microsoft Docs"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbe8297c459d4513d1b8e45c7d64807e0d73b503
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Administrar vários servidores usando os Servidores Centrais de Gerenciamento
  Você pode administrar vários servidores designando servidores de gerenciamento centrais e criando grupos de servidores.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>O que é um Servidor de Gerenciamento Central e grupos de servidores?  
 Uma instância do SQL Server, designada como um Servidor de Gerenciamento Central, mantém grupos de servidores que contêm as informações de conexão de uma ou mais instâncias. É possível executar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] e políticas de Gerenciamento Baseado em Políticas ao mesmo tempo nos grupos de servidores. Também é possível exibir os arquivos de log em instâncias gerenciadas por meio de um Servidor de Gerenciamento Central. 
 
 Basicamente, um Servidor de Gerenciamento Central é um repositório central que contém uma lista dos servidores gerenciados. As versões anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] não podem ser designadas como um Servidor de Gerenciamento Central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] também podem ser executadas nos grupos de servidor locais em Servidores Registrados.  
  
## <a name="create-central-management-server-and-server-groups"></a>Criar um Servidor de Gerenciamento Central e grupos de servidores 
 Para criar um Servidor de Gerenciamento Central e grupos de servidores, use a janela **Servidores Registrados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que o Servidor Central de Gerenciamento não pode ser membro de um grupo que o mantém. 
 
 Para saber como criar Servidores de Gerenciamento Central e grupos de servidores, consulte [Criar um Servidor de Gerenciamento Central e grupo de servidores &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

