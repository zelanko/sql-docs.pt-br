---
title: Compreender a propriedade do diagrama de banco de dados (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd71d87c5a2967d23f72b7402c7ca95a8822b688
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Compreender a propriedade do diagrama de banco de dados (Visual Database Tools)
Para usar o Designer de Diagrama de Banco de Dados, ele precisa ser configurado primeiramente por um membro da função db_owner (função de bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]) para controle do acesso a diagramas. Cada diagrama tem um e apenas um proprietário, o usuário que o criou. Para obter mais informações sobre como configurar a diagramação, consulte [Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md).  
  
Pontos de destaque sobre propriedade de diagrama:  
  
-   Embora qualquer usuário com acesso a um banco de dados possa criar um diagrama, depois de criado, os únicos usuários que podem exibi-lo são o designer do diagrama e os membros da função db_owner.  
  
-   A propriedade de diagramas só pode ser transferida para membros da função db_owner. Isso é possível apenas depois que o proprietário anterior do diagrama tiver sido removido do banco de dados.  
  
-   Se o proprietário de um diagrama for removido do banco de dados, o diagrama permanecerá no banco de dados até que um membro da função db_owner tente abri-lo. Nesse momento, o membro db_owner pode assumir a propriedade do diagrama.  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com diagramas de banco de dados (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  

