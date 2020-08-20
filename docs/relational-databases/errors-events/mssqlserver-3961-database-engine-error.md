---
description: MSSQLSERVER_3961
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 837215560e15ff01a84f614ac087ff96930db3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456111"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|3961|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XACT_METADATA_INVALID|  
|Texto da mensagem|Falha na transação de isolamento de instantâneo no banco de dados '%.*ls' porque o objeto acessado pela instrução foi modificado por uma instrução DDL em outra transação simultânea desde o início dessa transação.  Ela não é permitida porque os metadados não têm controle de versão. Uma atualização simultânea dos metadados poderá gerar inconsistências se for combinada ao isolamento de instantâneo.|  
  
## <a name="explanation"></a>Explicação  
Esse erro poderá ocorrer se você estiver consultando metadados do isolamento de instantâneo e houver uma instrução de DDL simultânea que atualiza os metadados que estão sendo acessados no isolamento de instantâneo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem suporte para controle de versão de metadados. Por esse motivo, há restrições nas operações de DDL que podem ser executadas em uma transação explícita sendo executada no isolamento de instantâneo. Por definição, uma transação implícita é uma instrução única que permite a imposição de semânticas de isolamento de instantâneo, mesmo com instruções de DDL. As instruções DDL a seguir não são permitidas sob o isolamento de instantâneo após uma instrução BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME ou qualquer instrução DDL do CLR (common language runtime). Essas instruções serão permitidas quando você estiver usando o isolamento de instantâneo em transações implícitas. Por definição, uma transação implícita é uma instrução única que permite a imposição de semânticas de isolamento de instantâneo, mesmo com instruções de DDL.  
  
## <a name="user-action"></a>Ação do usuário  
Altere o nível de isolamento do instantâneo a um nível de isolamento de não instantâneo como leitura confirmada antes de consultar os metadados.  
  
