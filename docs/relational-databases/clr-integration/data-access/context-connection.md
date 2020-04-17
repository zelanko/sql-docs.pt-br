---
title: Conexão contexto | Microsoft Docs
description: No Microsoft SQL Server, a conexão de contexto permite executar instruções Transact-SQL no mesmo contexto em que seu código foi invocado.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f29914557e3a1c1e7a929bec22a2b55d0db2a50
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485405"
---
# <a name="context-connection"></a>Conexão de contexto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O problema de acesso a dados internos é um cenário bastante comum. Ou seja, você deseja acessar o mesmo servidor no qual sua função ou seu procedimento armazenado CLR (Common Language Runtime) está em execução. Uma opção é criar uma conexão usando **System.Data.SqlClient.SqlConnection,** especificar uma seqüência de conexão que aponta para o servidor local e abrir a conexão. Isso exige a especificação de credenciais para fazer logon. A conexão está em uma sessão de banco de dados diferente do procedimento ou função armazenada, pode ter diferentes opções **SET,** está em uma transação separada, não vê suas tabelas temporárias, e assim por diante. Se código da função ou do procedimento armazenado gerenciado estiver em execução no processo do SQL Server, isso ocorrerá porque alguém se conectou a esse servidor e executou uma instrução SQL para invocá-lo. Você provavelmente deseja que o procedimento ou função armazenado seja executado no contexto dessa conexão, juntamente com sua transação, opções **SET** e assim por diante. Isto é chamado de conexão de contexto.  
  
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
 [Regular vs. Conexões de contexto](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Descreve as diferenças entre conexões normais e de contexto.  
  
 [Restrições em conexões comuns e de contexto](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Descreve as restrições em conexões normais e de contexto.  
  
  
