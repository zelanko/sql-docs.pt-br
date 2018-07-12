---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19e0e49ea3b9648600de6974d227fad3d25a728e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426405"
---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3961|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XACT_METADATA_INVALID|  
|Texto da mensagem|Falha na transação de isolamento de instantâneo no banco de dados '%.*ls' porque o objeto acessado pela instrução foi modificado por uma instrução DDL em outra transação simultânea desde o início dessa transação.  Isso não é permitido porque os metadados não têm controle de versão. Uma atualização simultânea para metadados poderia gerar inconsistências se misturada com isolamento de instantâneo.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro pode ocorrer se você estiver consultando metadados sob isolamento do instantâneo e tiver uma instrução DDL simultânea que atualiza os metadados que estão sendo acessados sob isolamento do instantâneo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem suporte para controle de versão de metadados. Por isso, há restrições nas operações DDL que podem ser executadas em uma transação explícita que está sendo executada sob isolamento do instantâneo. Uma transação implícita, por definição, é uma instrução única que torna possível impor semânticas de isolamento do instantâneo, até mesmo com instruções DDL. As instruções de DDL a seguir não são permitidas sob isolamento do instantâneo depois de uma instrução BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME ou qualquer instrução CRL (Common Language Runtime) DDL. Essas instruções são permitidas quando você está usando isolamento do instantâneo em transações implícitas. Uma transação implícita, por definição, é uma instrução única que torna possível impor semânticas de isolamento do instantâneo, até mesmo com instruções DDL.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere o nível de isolamento do instantâneo a um nível de isolamento de não instantâneo como leitura confirmada antes de consultar os metadados.  
  
  
