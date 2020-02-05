---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79b6637bcfa0c3484de5d4438c48abbec35e40d5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056642"
---
# <a name="mssqlserver_21898"></a>MSSQLSERVER_21898
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21898|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21898|  
|Texto da mensagem|O publicador '%s' usa o banco de dados de distribuição '%s', e não '%s', que é necessário para hospedar o banco de dados de publicação '%s'. Execute **sp_changedistpublisher** no distribuidor '%s' para alterar o banco de dados de distribuição usado pelo publicador para '%s'.|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_redirected_publisher** consulta msdb.dbo.MSdistpublishers no distribuidor local para verificar se o banco de dados de distribuição usado pelo novo publicador é igual ao banco de dados de distribuição usado pelo publicador original. Este erro é retornado quando esses bancos de dados são diferentes, tornando o publicador um host inadequado para o banco de dados publicador.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o procedimento armazenado **sp_changedistpublisher** para alterar o banco de dados de distribuição do novo publicador para o utilizado pelo publicador original.  
  
> [!NOTE]  
> A execução de **sp_changedistpublisher** resolverá o problema se o banco de dados de distribuição incorreto tiver sido inserido quando **sp_adddistpublisher** foi executado no distribuidor do publicador. No entanto, se o publicador remoto tiver publicações existentes de outro banco de dados de publicação que utilizam o banco de dados de distribuição identificado, essa alteração não será apropriada. A replicação que usa o banco de dados de distribuição nomeado precisa ser removida sistematicamente e restabelecida através do banco de dados de distribuição do editor original para que o novo editor funcione como um host satisfatório.  
  
