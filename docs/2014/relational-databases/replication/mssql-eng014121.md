---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfbdb88b67f2f0764b39a9968cc71e72a1d3ac3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155967"
---
# <a name="mssqleng014121"></a>MSSQL_ENG014121
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14121|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar o Distribuidor '%s'. Esse Distribuidor possui bancos de dados de distribuição associados.|  
  
## <a name="explanation"></a>Explicação  
 Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como Distribuidor não pode ser removida da função de Distribuidor porque existem bancos de dados de distribuição associados a essa instância. Esse erro ocorre ao tentar descartar um banco de dados de distribuição associado a um ou mais Publicadores.  
  
## <a name="user-action"></a>Ação do usuário  
 Para encontrar os nomes de Publicadores e os bancos de dados de distribuição associados a um Distribuidor, execute [sp_helpdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql) em qualquer banco de dados no Distribuidor.  
  
 Execute [sp_dropdistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql) em um banco de dados de distribuição associado a esse Distribuidor. Após todas as associações de banco de dados de distribuição serem removidas, é possível desabilitar a distribuição.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)   
 [Configurar Distribuição](configure-distribution.md)  
  
  
