---
title: Administrar vários servidores usando os Servidores Centrais de Gerenciamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f47eec543c21e74565d750035d20fbcee9baa82e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877298"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Administrar vários servidores usando os Servidores Centrais de Gerenciamento
  Você pode administrar vários servidores designando servidores de gerenciamento centrais e criando grupos de servidores.  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>Benefícios dos Servidores Centrais de Gerenciamento e grupos de servidores  
 Uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], que é designada como um Servidor Central de Gerenciamento, mantém grupos de servidores que contêm as informações de conexão de uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. As instruções [!INCLUDE[tsql](../includes/tsql-md.md)] e as políticas de gerenciamento baseado em política podem ser executadas ao mesmo tempo nos grupos de servidores. Você também pode exibir os arquivos de log [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em instâncias que são gerenciadas por um Servidor de Gerenciamento Central. As versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] não podem ser designadas como um Servidor de Gerenciamento Central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] também podem ser executadas nos grupos de servidor locais em Servidores Registrados.  
  
### <a name="related-tasks"></a>Related Tasks  
 Para criar um Servidor de Gerenciamento Central e grupos de servidores, use a janela **Servidores Registrados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que o Servidor Central de Gerenciamento não pode ser membro de um grupo que o mantém. Para obter mais informações sobre como criar Servidores de Gerenciamento Central e grupos de servidores, consulte [Criar um Servidor de Gerenciamento Central e Grupo de Servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
