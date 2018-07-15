---
title: Modificar instruções UPDATETEXT que leem e gravam objetos binários grandes (BLOBs) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85036a4d91fc426a0195c4fd589fbddcadfb5da4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234326"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>Modificar instruções UPDATETEXT que leem e gravam em BLOBs (objetos grandes binários)
  O Supervisor de Atualização detectou instruções UPDATETEXT que leem e gravam no mesmo BLOB (objeto binário grande) usando o mesmo ponteiro de texto. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não oferece suporte para o uso de ponteiros de texto dessa forma.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Copie o BLOB para uma tabela temporária ou variável de tabela e, em seguida, atribua os valores novamente às colunas originais.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
