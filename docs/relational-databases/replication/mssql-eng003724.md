---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1f597a76f2f94acbfeb3647a01da0d2183b99ad2
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362746"
---
# <a name="mssql_eng003724"></a>MSSQL_ENG003724
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|3724|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não é possível %S_MSG o %S_MSG '%.*ls' porque está sendo usado para replicação.|  
  
## <a name="explanation"></a>Explicação  
 Quando os objetos em um banco de dados são replicados, são marcados como replicados na tabela do sistema **sysarticles** (para publicações de instantâneo e transacionais) ou **sysmergearticles** (para publicações de mesclagem). Se tentar descartar um objeto replicado, ocorrerá esse erro.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de que o objeto de banco de dados não está replicado antes de tentar descartá-lo. Por exemplo:  
  
-   Se o erro ocorrer no banco de dados de publicação, descarte o artigo da publicação antes de descartar o objeto. Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
-   Se o erro ocorrer no banco de dados de assinatura, descarte a assinatura antes de descartar o objeto. Para obter mais informações, consulte [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md) (Assinar publicações). Para assinaturas de publicações transacionais, é possível descartar a assinatura de um artigo individual em vez de toda a publicação. Para obter mais informações, consulte [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Se esse erro ocorrer em um banco de dados não replicado, execute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para garantir que os objetos nos bancos de dados não são marcados como replicados.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
