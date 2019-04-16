---
title: Altera o comportamento de sinalizadores de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 421420089526540929bfc4ade32799634a823391
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582539"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Alterações no comportamento de sinalizadores de rastreamento
  Sinalizadores de rastreamento globais definidos por uma sessão afetam outras sessões imediatamente. Alguns sinalizadores de rastreamento do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] não existem no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Recomendamos que você desabilite todos os sinalizadores de rastreamento antes de atualizar. Sinalizadores de rastreamento que modificam os modos de disponibilidade ou recuperação de banco de dados podem impedir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] atualize com êxito a sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você poderá habilitar os sinalizadores de rastreamento depois de verificar se eles são necessários e continuam válidos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se precisar habilitar novamente esses sinalizadores de rastreamento, será necessário fazer testes adicionais em sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte a sinalizadores de rastreamento no nível de sessão e globais. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os sinalizadores de rastreamento podem ser especificados tanto como locais quanto como globais usando o argumento adicional (-1) no comando DBCC TRACEON. Se esse argumento não for especificado, o valor padrão será local.  
  
 Além disso, no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], um sinalizador de rastreamento definido na sessão A não entram em vigor automaticamente em uma sessão b existente. Em vez disso, esse sinalizador de rastreamento entrará em vigor somente após a primeira vez em que nenhum sinalizador de rastreamento é definido na sessão B. Esse comportamento é não determinístico no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e é determinístico no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, onde os sinalizadores de rastreamento global definidos na sessão A são definidos imediatamente nas outras sessões simultâneas.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
