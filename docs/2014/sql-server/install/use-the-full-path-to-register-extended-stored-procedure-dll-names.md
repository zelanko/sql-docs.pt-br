---
title: Use o caminho completo para registrar nomes de DLL de procedimento armazenado estendido | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- registering DLL names
- extended stored procedures [SQL Server], registering
- DLL names [SQL Server]
- full path DLL name registration [SQL Server]
ms.assetid: f648d57c-af32-4c71-9882-47b6766f3c2b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5ec4ef3fc2e0f2c4834ffa7479a00562ae15d07f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058832"
---
# <a name="use-the-full-path-to-register-extended-stored-procedure-dll-names"></a>Usar caminho completo para registrar nomes de DLL de procedimentos armazenados estendidos
  Procedimentos armazenados estendidos que foram registrados anteriormente sem um caminho completo para o nome de DLL podem não funcionar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Procedimentos armazenados estendidos que foram registrados anteriormente sem um caminho completo para o nome de DLL podem não funcionar depois da atualização. Isso é porque o diretório BINN antigo não é adicionado ao novo caminho durante o processo de atualização. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode não conseguir localizar os procedimentos armazenados estendidos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes da atualização, faça as etapas a seguir para cada procedimento armazenado estendido que não foi registrado com um nome de caminho completo:  
  
1.  Execute sp_dropextendedproc para remover o procedimento armazenado estendido.  
  
2.  Execute sp_addextendedproc para registrar o procedimento armazenado estendido com o nome de caminho completo.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
