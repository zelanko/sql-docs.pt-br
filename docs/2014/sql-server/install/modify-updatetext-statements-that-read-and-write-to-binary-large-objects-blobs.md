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
ms.topic: article
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5b0c6df5c9324a35f1f642d366ef8f2780341592
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117808"
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
  
  
