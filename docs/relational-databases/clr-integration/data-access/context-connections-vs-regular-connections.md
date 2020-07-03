---
title: Conexões regulares vs. de contexto | Microsoft Docs
description: Em SQL Server, às vezes você deve usar conexões regulares para instruções Transact-SQL, mas as conexões de contexto oferecem vantagens de uso de recursos e desempenho.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: 4beff218c544e86d6c9f0ee45957bbd6b1d4691a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882599"
---
# <a name="context-connections-vs-regular-connections"></a>Conexões de contexto versus conexões regulares
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Se você estiver conectando a um servidor remoto, sempre use conexões normais, em vez de conexões de contexto. Se você precisar se conectar ao mesmo servidor em que o procedimento armazenado ou a função está sendo executado, use a conexão de contexto na maioria dos casos. Isto tem benefícios, como executar no mesmo espaço de transação e não precisar se autenticar novamente.  
  
 Além disso, o uso da conexão de contexto normalmente resulta em melhor desempenho e menos uso de recurso. A conexão de contexto é uma conexão somente em processo, portanto, ela pode entrar em contato com o servidor "diretamente", ignorando as camadas de protocolo de rede e transporte para enviar instruções Transact-SQL e receber resultados. O processo de autenticação é ignorado também. A figura a seguir mostra os principais componentes do provedor gerenciado **SqlClient** , bem como como os diferentes componentes interagem entre si ao usar uma conexão regular e ao usar a conexão de contexto.  
  
 ![Caminhos de código de um contexto e uma conexão regular.](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Caminhos de código de um contexto e uma conexão regular.")  
  
 A conexão de contexto segue um caminho de código mais curto e envolve menos componentes. Dessa forma, você pode esperar que as solicitações e os resultados sejam enviados e recebidos do servidor mais rapidamente do que em uma conexão normal. O tempo de execução da consulta no servidor é o mesmo para conexões de contexto e normais.  
  
 Há alguns casos em que você pode precisar abrir uma conexão normal separada para o mesmo servidor. Por exemplo, há certas restrições no uso da conexão de contexto, descritas em [restrições em conexões regulares e de contexto](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
