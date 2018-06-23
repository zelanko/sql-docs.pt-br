---
title: Alterações no comportamento em syslockinfo e sp_lock | Microsoft Docs
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
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 982f31bbffb32726089fa331d105bfc262fc16a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010329"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Alterações no comportamento em syslockinfo e sp_lock
  O**syslockinfo** e o **sp_lock** podem retornar valores inesperados. Eles também podem retornar linhas adicionais, enquanto que versões anteriores de **syslockinfo** e **sp_lock** retornavam, no máximo, duas linhas por recurso de bloqueio.  
  
 Para acessar informações de **syslockinfo** ou executar **sp_lock** , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], o **rsc_objid** e **rsc_indid** colunas em **syslockinfo** e **objid** e **indid**  colunas em **sp_lock** consistentemente retornar a ID de objeto e a identificação do índice. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o valor 0 pode ser retornado.  
  
 Em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** e **sp_lock** retornar um máximo de duas linhas para qualquer recurso de bloqueio em uma única transação. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], quando o particionamento de bloqueio passou a ser habilitado, várias linhas podem ser retornadas para o mesmo recurso executado em uma transação. Há podem ser até N + 1 linhas retornadas, onde N é o número de CPUs. Além disso, agora é possível ter as solicitações GRANTED e WAITING exibidas para o mesmo recurso, o que não era possível no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
