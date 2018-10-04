---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62c5300561cf70462402692d03f53f2de860781a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131172"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3724|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível %S_MSG o %S_MSG '%.*ls' porque está sendo usado para replicação.|  
  
## <a name="explanation"></a>Explicação  
 Quando os objetos em um banco de dados são replicados, são marcados como replicados na tabela do sistema **sysarticles** (para publicações de instantâneo e transacionais) ou **sysmergearticles** (para publicações de mesclagem). Se tentar descartar um objeto replicado, ocorrerá esse erro.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de que o objeto de banco de dados não está replicado antes de tentar descartá-lo. Por exemplo:  
  
-   Se o erro ocorrer no banco de dados de publicação, descarte o artigo da publicação antes de descartar o objeto. Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
-   Se o erro ocorrer no banco de dados de assinatura, descarte a assinatura antes de descartar o objeto. Para obter mais informações, consulte [Subscribe to Publications](subscribe-to-publications.md) (Assinar publicações). Para assinaturas de publicações transacionais, é possível descartar a assinatura de um artigo individual em vez de toda a publicação. Para obter mais informações, consulte [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql).  
  
 Se esse erro ocorrer em um banco de dados não replicado, execute [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) para garantir que os objetos nos bancos de dados não são marcados como replicados.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
