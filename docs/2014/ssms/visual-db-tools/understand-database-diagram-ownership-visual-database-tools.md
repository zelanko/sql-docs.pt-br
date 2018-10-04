---
title: Compreender a propriedade do diagrama de banco de dados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0fef70305887b7d0b2d5face1dc31a2e7ea451c6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102446"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Compreender a propriedade do diagrama de banco de dados (Visual Database Tools)
  Para usar o Designer de Diagrama de Banco de Dados, ele precisa ser configurado primeiramente por um membro da função db_owner (função de bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) para controle do acesso a diagramas. Cada diagrama tem um e apenas um proprietário, o usuário que o criou. Para obter mais informações sobre como configurar a diagramação, consulte [definir o Designer de diagramas de banco de dados &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Pontos de destaque sobre propriedade de diagrama:  
  
-   Embora qualquer usuário com acesso a um banco de dados possa criar um diagrama, depois de criado, os únicos usuários que podem exibi-lo são o designer do diagrama e os membros da função db_owner.  
  
-   A propriedade de diagramas só pode ser transferida para membros da função db_owner. Isso é possível apenas depois que o proprietário anterior do diagrama tiver sido removido do banco de dados.  
  
-   Se o proprietário de um diagrama for removido do banco de dados, o diagrama permanecerá no banco de dados até que um membro da função db_owner tente abri-lo. Nesse momento, o membro db_owner pode assumir a propriedade do diagrama.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](work-with-database-diagrams-visual-database-tools.md)   
 [Configurar o Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
