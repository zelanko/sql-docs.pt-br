---
title: Remover dois pontos após a palavra-chave reservada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce2cfce6e35a95b7a07c17c4d3a2fd8a1b1c2610
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093177"
---
# <a name="remove-colon-following-reserved-keyword"></a>Remover dois-pontos após palavra-chave reservada
  O Supervisor de Atualização detectou um script que contém dois-pontos (:) depois de uma palavra-chave reservada. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa sintaxe era ignorada e as instruções eram executadas corretamente. Agora, essa sintaxe faz com que a instrução falhe quando o modo de compatibilidade de banco de dados está definido como 100 ou posterior.  
  
 Os bancos de dados de usuário mantêm o modo de compatibilidade.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes de alterar o modo de compatibilidade do banco de dados para 100 ou posterior, modifique seus scripts removendo os dois-pontos depois das palavras-chave reservadas. Para obter mais informações, consulte ‘sp_dbcmptlevel’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
