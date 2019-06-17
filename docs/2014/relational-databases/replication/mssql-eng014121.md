---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 996b93f04d9e9fc063bbacbb5f4a7588794ad208
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191508"
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
  
  
