---
title: Gatilho AFTER aninhado dispara até mesmo quando aninhamento de gatilho é OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 826961aef9133c001c643c1ee7058d01438fe868
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098416"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>Gatilho AFTER aninhado dispara até mesmo quando aninhamento de gatilho está definido como OFF
  O Supervisor de Atualização detectou um gatilho AFTER aninhado dentro de um gatilho INSTEAD OF que está defino em uma ou mais tabelas. Gatilhos AFTER aninhados podem disparar quando a opção de configuração do servidor `nested triggers` está definida como 0.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 O primeiro gatilho AFTER aninhado dentro de um gatilho INSTEAD OF é disparado mesmo se a opção de configuração do servidor `nested triggers` estiver definida como 0. Porém, nessa configuração, gatilhos AFTER subsequentes não disparam.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Revise seus aplicativos para verificar se há gatilhos aninhados. Verifique se os aplicativos ainda estão de acordo com as regras de negócio com relação a esse novo comportamento quando a opção de configuração do servidor `nested triggers` está definida como 0 e faça as modificações apropriadas.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
