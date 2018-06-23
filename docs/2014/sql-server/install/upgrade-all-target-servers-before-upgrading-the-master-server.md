---
title: Atualize todos os servidores de destino antes de atualizar o servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fdd218b1d5bfaacaffbd50c50d55dd47d613d207
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116858"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>Atualizar todos os servidores de destino antes da atualização do servidor mestre
  Antes de você atualizar o servidor mestre, atualize todos os computadores que estão executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estão configurados como servidores de destino.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Description  
 Para automatizar a administração em ambientes com vários servidores, é necessário ter pelo menos um servidor mestre e um servidor de destino. Um servidor mestre distribui trabalhos para servidores de destino e também recebe eventos desses servidores. Ele também armazena a cópia central das definições de trabalho para trabalhos que são executados em servidores de destino.  
  
 Se o servidor atual estiver configurado como servidor mestre, atualize todos os seus servidores de destino antes de atualizar o servidor mestre.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Se não for possível atualizar todos os servidores de destino antes de atualizar o servidor mestre, você deve remover todos os servidores de destino e reinscrevê-los depois da atualização.  
  
 Para obter mais informações, consulte os tópicos ‘Automatizando a administração em uma empresa’, "Como remover um servidor de destino de um servidor mestre’ e ‘Como inscrever um servidor de destino em um mestre’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  