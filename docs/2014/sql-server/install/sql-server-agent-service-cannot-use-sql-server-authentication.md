---
title: O serviço de SQL Server Agent não pode usar a autenticação SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e16882247a123b32ba07fbbae0d1f3573fd2d678
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092065"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>Serviço do SQL Server Agent não pode usar a Autenticação do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent aceita Autenticação do Windows somente quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent conecta-se com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>DESCRIÇÃO  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent somente pode fazer logon no banco de dados usando a Autenticação do Windows. Isso significa que a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte os tópicos ‘Segurança para administração automática’ e ‘Implementando segurança no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
