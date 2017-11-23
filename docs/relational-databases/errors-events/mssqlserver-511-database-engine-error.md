---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24f911f8f104737a51b5628e74ee3e0da8bcfbe5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|511|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ROW_TOOBIG|  
|Texto da mensagem|Não é possível criar uma linha com o tamanho %d que seja maior que o máximo permitido de %d.|  
  
## <a name="explanation"></a>Explicação  
A operação que você tentou excedeu o tamanho máximo de uma linha. Normalmente, o tamanho máximo de uma linha é de 8.060 bytes. Alguns formatos de armazenamento contêm sobrecarga que pode reduzir o tamanho de linha disponível para dados. Por exemplo, quando você usa colunas esparsas, o tamanho máximo de uma linha é de 8.018 bytes. Algumas operações que adicionam ou removem linhas e outras operações que alteram o tipo de dados de uma coluna exigem que a linha seja gravada novamente na página de dados e que a linha original seja posteriormente removida. Nessas operações, o limite efetivo do tamanho da linha é metade do limite máximo. Isso ocorre porque a linha original e a linha modificada devem ser incluídas na página de dados por um período curto.  
  
## <a name="user-action"></a>Ação do usuário  
Se for possível, reduza o tamanho da linha.  
  
Se considerar que o problema está sendo causado por uma atualização no local da linha, será necessário alterar a tabela em várias etapas. Crie uma tabela e transfira os dados para ela. Depois, exclua a tabela original e renomeie a tabela nova ou, então, trunque a tabela original, modifique as linhas na tabela original e, depois, mova os dados de volta para ela.  
  
