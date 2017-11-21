---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af5da3fbf06dea7712a03152b54bb65001ec2e42
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|905|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBSTARTUP_EE_PARTITIONING|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser iniciado nesta edição do SQL Server porque ele contém uma função de partição '%.\*ls'. Somente a edição Enterprise do SQL Server oferece suporte ao particionamento.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados contém uma ou mais tabelas ou índices particionados. Esta edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode usar particionamento. Portanto, o banco de dados não pode ser iniciado corretamente. As tabelas e os índices particionados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="user-action"></a>Ação do usuário  
Desanexe o banco de dados usando o procedimento armazenado sp_detach_db. Mova os arquivos, se necessário, e anexe o banco de dados a uma instância de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte usando CREATE DATABASE com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Desabilite o particionamento em todas as tabelas e remova as funções de particionamento. Desanexe e anexe novamente o banco de dados ao servidor atual.  
  

