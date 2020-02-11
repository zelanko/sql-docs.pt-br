---
title: Especifique a palavra-chave WITH ao usar dicas de tabela no modo de compatibilidade 90 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff2fee26c6f71cc398f8dbacf91f3ad8dbdb3358
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092157"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>Especificar a palavra-chave WITH ao usar dicas de tabela no modo de compatibilidade 90
  Com algumas exceções, há suporte para dicas de tabela na cláusula FROM de uma consulta somente quando as dicas são especificadas usando a palavra-chave WITH. Para obter mais informações, consulte os tópicos ‘FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])’ e ‘Dicas de tabela ([!INCLUDE[tsql](../../includes/tsql-md.md)]) ’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique as consultas que incluem dicas de tabela na cláusula FROM incluindo a palavra-chave WITH antes das dicas de tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
