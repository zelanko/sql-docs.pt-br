---
title: O serviço do SQL Server Agent não é possível usar a autenticação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d9badd521bf9bdccd5c141e28956f5b19f6275d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119716"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>Serviço do SQL Server Agent não pode usar a Autenticação do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent aceita Autenticação do Windows somente quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent conecta-se com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Description  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent somente pode fazer logon no banco de dados usando a Autenticação do Windows. Isso significa que a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte os tópicos ‘Segurança para administração automática’ e ‘Implementando segurança no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
