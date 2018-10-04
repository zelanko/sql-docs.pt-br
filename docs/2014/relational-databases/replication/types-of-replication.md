---
title: Tipos de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2fa6d02a8fc501f4b196c175056f18f7a9bff7c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162386"
---
# <a name="types-of-replication"></a>Tipos de replicação
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece os seguintes tipos de replicação para uso nos aplicativos distribuídos:  
  
-   Replicação transacional. Para obter mais informações, consulte [Replicação transacional](transactional/transactional-replication.md).  
  
-   Replicação de mesclagem. Para obter mais informações, consulte [Replicação de mesclagem](merge/merge-replication.md).  
  
-   Replicação de instantâneo Para obter mais informações, consulte [Replicação de instantâneo](snapshot-replication.md).  
  
 O tipo de replicação que você escolhe para um aplicativo, depende de muitos fatores, incluindo o ambiente físico da replicação, o tipo e a quantidade de dados a serem replicados e se os dados serão ou não atualizados no Assinante. O ambiente físico inclui o número e local dos computadores envolvidos na replicação e se esses computadores são clientes (estações de trabalho, laptops ou dispositivos portáteis) ou servidores.  
  
 Cada tipo de replicação começa normalmente com uma sincronização inicial dos objetos publicados entre o Publicador e os Assinantes. Esta sincronização inicial pode ser executada por replicação com um *instantâneo*, que é uma cópia de todos os objetos e dados especificados por uma publicação. Depois que o instantâneo é criado, ele é distribuído aos Assinantes. Para alguns aplicativos, a replicação de instantâneo é tudo o que é necessário. Para outros tipos de aplicativos, é importante que as alterações de dados subsequentes fluam para o Assinante de forma incremental com o passar do tempo. Alguns aplicativos também exigem que as alterações fluam do Assinante de volta para o Publicador. A replicação transacional e a replicação de mesclagem fornecem opções para estes tipos de aplicativos.  
  
 As alterações de dados não são rastreadas para a replicação de instantâneo. Sempre que um instantâneo é aplicado, ele sobrescreve por completo os dados existentes. A replicação transacional rastreia as alterações pelo log de transação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a replicação de mesclagem rastreia as alterações pelos gatilhos e tabelas de metadados.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos agentes de replicação.](agents/replication-agents-overview.md)  
  
  
