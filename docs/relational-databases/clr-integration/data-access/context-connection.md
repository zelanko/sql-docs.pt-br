---
title: Conexão de contexto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: afe4fd0360b6ba50db7e007e6c3e6fbc78c3060f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="context-connection"></a>Conexão de contexto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O problema de acesso a dados internos é um cenário bastante comum. Ou seja, você deseja acessar o mesmo servidor no qual sua função ou seu procedimento armazenado CLR (Common Language Runtime) está em execução. Uma opção é criar uma conexão usando **SqlConnection**, especifique uma cadeia de caracteres de conexão que aponta para o servidor local e abrir a conexão. Isso exige a especificação de credenciais para fazer logon. A conexão está em uma sessão de banco de dados diferente do procedimento armazenado ou função, pode ter diferentes **definir** opções, está em uma transação separada, não vê suas tabelas temporárias e assim por diante. Se código da função ou do procedimento armazenado gerenciado estiver em execução no processo do SQL Server, isso ocorrerá porque alguém se conectou a esse servidor e executou uma instrução SQL para invocá-lo. Você provavelmente deseja que o procedimento armazenado ou função a ser executada no contexto dessa conexão, juntamente com sua transação **definir** opções e assim por diante. Isto é chamado de conexão de contexto.  
  
 A conexão de contexto permite executar instruções Transact-SQL no mesmo contexto em que seu código foi invocado pela primeira vez. Para obter a conexão de contexto, use a palavra-chave de cadeia de conexão "context connection", como no exemplo a seguir:  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>Nesta seção  
 [Vs regulares. Conexões de contexto](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Descreve as diferenças entre conexões normais e de contexto.  
  
 [Restrições em conexões de contexto e normais](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Descreve as restrições em conexões normais e de contexto.  
  
  
