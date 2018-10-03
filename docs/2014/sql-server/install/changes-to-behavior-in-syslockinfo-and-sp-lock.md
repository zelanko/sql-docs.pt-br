---
title: Alterações no comportamento em syslockinfo e sp_lock | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6dfe3901cb23cff65dd96fa084232310ef91ede
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104566"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Alterações no comportamento em syslockinfo e sp_lock
  O**syslockinfo** e o **sp_lock** podem retornar valores inesperados. Eles também podem retornar linhas adicionais, enquanto que versões anteriores de **syslockinfo** e **sp_lock** retornavam, no máximo, duas linhas por recurso de bloqueio.  
  
 Para acessar informações de **syslockinfo** ou executar **sp_lock** , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Na [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], o **rsc_objid** e **rsc_indid** colunas **syslockinfo** e o **objid** e **indid**  colunas no **sp_lock** consistentemente retornar a ID de objeto e identificação do índice. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o valor 0 pode ser retornado.  
  
 Na [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** e **sp_lock** retornar no máximo duas linhas para qualquer recurso de bloqueio em uma única transação. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], quando o particionamento de bloqueio passou a ser habilitado, várias linhas podem ser retornadas para o mesmo recurso executado em uma transação. Lá podem ser até N + 1 linhas retornadas, onde N é o número de CPUs. Além disso, agora é possível ter as solicitações GRANTED e WAITING exibidas para o mesmo recurso, o que não era possível no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
