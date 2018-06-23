---
title: Não há suporte para WITH CHECK OPTION em modos de exibição que contenham TOP no modo de compatibilidade 90 ou posterior | Microsoft Docs
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
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0dde9e879d278455544d4f323a8f3ffdd492760d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006033"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>Não há suporte para WITH CHECK OPTION em exibições que contenham TOP no modo de compatibilidade 90 ou posterior
  O Supervisor de Atualização detectou uma exibição que usa o WITH CHECK OPTION e uma cláusula TOP na instrução SELECT da exibição ou em uma exibição referenciada. Exibições definidas dessa forma permitem, incorretamente, que os dados sejam modificados através da exibição; isso pode gerar resultados imprecisos quando o modo de compatibilidade do banco de dados está definido como 80 ou anterior. Não é possível inserir ou atualizar dados através de uma exibição que usa WITH CHECK OPTION quando a exibição ou uma exibição referenciada usa a cláusula TOP e o modo de compatibilidade do banco de dados está definido como 90 ou posterior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Quando você faz a atualização, os bancos de dados de usuários mantêm seus modos de compatibilidade. Antes de alterar o modo de compatibilidade do banco de dados para 100 ou posterior, modifique as exibições que usam tanto WITH CHECK OPTION quanto TOP caso precise alterar dados através da exibição. Para obter mais informações, consulte [sp_dbcmptlevel &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
