---
title: Outros problemas de atualização de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
caps.latest.revision: 34
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1aa132e53e3d3328863c8f30fc86277fc6b394ea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200676"
---
# <a name="other-replication-upgrade-issues"></a>Outros problemas de atualização da replicação
  Este tópico aborda uma série de problemas de atualização que não são relatados pelo Supervisor de Atualização.  
  
## <a name="versions-supported"></a>Versões com suporte  
 O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte a atualizações de bancos de dados replicados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você não precisa interromper a atividade de outros nós enquanto um nó está sendo atualizado. Verifique se você está de acordo com as regras relacionadas a versões que têm suporte em uma topologia.  
  
 Normalmente, ao fazer a replicação entre diferentes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você ficará limitado à funcionalidade da versão anterior que está sendo usada.  
  
> [!NOTE]  
>  Como o formato de armazenamento em disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o mesmo em ambientes de 64 e 32 bits, a topologia de replicação pode combinar instâncias de servidor executadas em um ambiente de 32 bits e instâncias de servidor executadas em um ambiente de 64 bits.  
  
 Para todos os tipos de replicação, a versão do Distribuidor não pode ser anterior à versão do Publicador. (Normalmente, o Distribuidor faz parte da mesma instância que o Publicador.)  
  
 Para a replicação transacional, um Assinante de uma publicação transacional pode ser de qualquer uma das duas versões do Publicador.  
  
 Para replicação de mesclagem, um Assinante de uma publicação de mesclagem pode ser de qualquer versão anterior à versão do publicador.  
  
## <a name="merge-replication-batches-changes"></a>Alterações em lotes da replicação de mesclagem  
 As alterações que são feitas pelo Agente de Mesclagem são divididas em lotes para aprimorar o desempenho; assim, mais de uma linha pode ser inserida, atualizada ou excluída em uma única instrução. Se alguma tabela publicada nos bancos de dados de publicação ou de assinatura tiver gatilhos, verifique se os gatilhos conseguem lidar com inserções, atualizações e exclusões multilinha. Para obter mais informações, consulte "Considerações multilinha para gatilhos DML" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="activex-control-changes"></a>Alterações do controle ActiveX  
 As seguintes alterações foram feitas para controles ActiveX de replicação:  
  
-   Todos os controles ActiveX são marcados como inseguros para gerar script e para inicialização.  
  
-   O controle ActiveX de Instantâneo foi descartado. Você pode criar e gerenciar instantâneos usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou programaticamente usando procedimentos armazenados de replicação. Para obter mais informações, consulte os tópicos "Como criar e aplicar o instantâneo inicial ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])" e "Como criar o instantâneo inicial (Programação Transact-SQL de replicação)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O controle ActiveX de Distribuição e o controle ActiveX de Mesclagem foram preteridos. Uma funcionalidade semelhante é fornecida por aplicativos de código gerenciado que usam RMO (Replication Management Objects). Para obter mais informações, consulte "Sincronizando assinaturas (Programação RMO)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas na atualização da replicação](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
