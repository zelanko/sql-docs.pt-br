---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 551b199b6c4c97b58eca822e1372d3b51af31585
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423455"
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21898|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21898|  
|Texto da mensagem|O publicador '%s' usa o banco de dados de distribuição '%s', e não '%s', que é necessário para hospedar o banco de dados de publicação '%s'. Execute `sp_changedistpublisher` no distribuidor '%s' para alterar o banco de dados de distribuição usado pelo publicador para '%s'.|  
  
## <a name="explanation"></a>Explicação  
 `sp_validate_redirected_publisher` consultas msdistpublishers no distribuidor local para verificar se o banco de dados de distribuição usado pelo novo publicador é o mesmo que o banco de dados de distribuição usado pelo publicador original. Este erro é retornado quando esses bancos de dados são diferentes, tornando o publicador um host inadequado para o banco de dados publicador.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute o procedimento armazenado `sp_changedistpublisher` para alterar o banco de dados de distribuição do novo publicador para o utilizado pelo publicador original.  
  
> [!NOTE]  
>  A execução de `sp_changedistpublisher` tratará o problema se o banco de dados de distribuição incorreto tiver sido inserido quando `sp_adddistpublisher` foi executado no distribuidor do publicador. No entanto, se o publicador remoto tiver publicações existentes de outro banco de dados de publicação que utilizam o banco de dados de distribuição identificado, essa alteração não será apropriada. A replicação que usa o banco de dados de distribuição nomeado precisa ser removida sistematicamente e restabelecida através do banco de dados de distribuição do publicador original para que o novo publicador funcione como um host satisfatório.  
  
  
