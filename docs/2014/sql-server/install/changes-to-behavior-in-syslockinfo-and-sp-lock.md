---
title: Alterações no comportamento em syslockinfo e sp_lock | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8c6534449ffc4e89efcd49c943726bf6ecd9f26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096653"
---
# <a name="changes-to-behavior-in-syslockinfo-and-sp_lock"></a>Alterações no comportamento em syslockinfo e sp_lock
  **syslockinfo** e **sp_lock** podem retornar valores inesperados. Eles também podem retornar linhas adicionais, enquanto que versões anteriores de **syslockinfo** e **sp_lock** retornavam, no máximo, duas linhas por recurso de bloqueio.  
  
 Para acessar informações de **syslockinfo** ou executar **sp_lock** , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], as colunas **rsc_objid** e **rsc_indid** no **syslockinfo** , e as colunas **objid** e **indid** no **sp_lock** retornam, consistentemente, a identificação do objeto e a identificação do índice. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o valor 0 pode ser retornado.  
  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** e **sp_lock** retornam, no máximo, duas linhas para qualquer recurso de bloqueio em uma única transação. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], quando o particionamento de bloqueio passou a ser habilitado, várias linhas podem ser retornadas para o mesmo recurso executado em uma transação. Pode haver até N + 1 linhas retornadas, em que N é o número de CPUs. Além disso, agora é possível ter as solicitações GRANTED e WAITING exibidas para o mesmo recurso, o que não era possível no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
