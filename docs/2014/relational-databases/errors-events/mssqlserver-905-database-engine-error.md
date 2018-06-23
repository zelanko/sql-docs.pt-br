---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d84961f4903ac6dd0a950ceaa8a8fb9368efcf6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021156"
---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
    
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
 O banco de dados contém uma ou mais tabelas ou índices particionados. Esta edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode usar particionamento. Portanto, o banco de dados não pode ser iniciado corretamente. As tabelas e os índices particionados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Desanexe o banco de dados usando o procedimento armazenado sp_detach_db. Mova os arquivos, se necessário, e anexe o banco de dados a uma instância de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte usando CREATE DATABASE com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Desabilite o particionamento em todas as tabelas e remova as funções de particionamento. Desanexe e anexe novamente o banco de dados ao servidor atual.  
  
  