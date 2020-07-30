---
title: MSSQL_ENG014120 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c2940a109a7288d332a80fd67291663831bfe262
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362594"
---
# <a name="mssql_eng014120"></a>MSSQL_ENG014120
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14120|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar o banco de dados de distribuição '%s'. O banco de dados do distribuidor está associado a um Publicador.|  
  
## <a name="explanation"></a>Explicação  
 O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Esse erro ocorre ao tentar descartar um banco de dados de distribuição associado a um ou mais Publicadores.  
  
## <a name="user-action"></a>Ação do usuário  
 Para descartar um banco de dados de distribuição, é necessário primeiro descartar a associação entre o Distribuidor e o Publicador. Para obter mais informações, consulte [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
