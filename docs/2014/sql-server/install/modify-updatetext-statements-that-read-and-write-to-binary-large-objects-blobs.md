---
title: Modificar instruções UPDATETEXT que lêem e gravam em BLOBs (objetos binários grandes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 061e7bad0bae5a74d103406265ad79195f79f7db
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059210"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>Modificar instruções UPDATETEXT que leem e gravam em BLOBs (objetos grandes binários)
  O Supervisor de Atualização detectou instruções UPDATETEXT que leem e gravam no mesmo BLOB (objeto binário grande) usando o mesmo ponteiro de texto. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não oferece suporte para o uso de ponteiros de texto dessa forma.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Copie o BLOB para uma tabela temporária ou variável de tabela e, em seguida, atribua os valores novamente às colunas originais.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
