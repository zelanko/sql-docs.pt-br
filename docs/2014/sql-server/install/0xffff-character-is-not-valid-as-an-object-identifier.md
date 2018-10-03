---
title: caractere 0xFFFF não é válido como um identificador de objeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a91a64358ccd23e923d30a291b044800ce710ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112764"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>Caractere 0xFFFF não é válido como um identificador de objeto
  O Supervisor de Atualização detectou o caractere 0xFFFF em um identificador de objeto. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, objetos como bancos de dados, tabelas e colunas que contêm esse caractere em seus identificadores não podem ser referenciados ou renomeados quando o modo de compatibilidade do banco de dados estiver definido como 90 ou posterior. Quando você faz a atualização para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], os bancos de dados mantêm seus modos de compatibilidade. Antes de você alterar o modo de compatibilidade do banco de dados para 90 ou posterior, renomeie o objeto que contém o caractere 0xFFFF.  
  
 Para obter mais informações sobre os identificadores, consulte ‘Identificadores’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre modos de compatibilidade de banco de dados, consulte ‘sp_dbcmptlevel’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
