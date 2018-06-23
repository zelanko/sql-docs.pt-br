---
title: Vs regulares. Conexões de contexto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8758f1e7c680af9d546ba2b9894304388a01e46d
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696913"
---
# <a name="context-connections-vs-regular-connections"></a>Vs de conexões de contexto. Conexões normais
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se você estiver conectando a um servidor remoto, sempre use conexões normais, em vez de conexões de contexto. Se você precisar se conectar ao mesmo servidor em que o procedimento armazenado ou a função está sendo executado, use a conexão de contexto na maioria dos casos. Isto tem benefícios, como executar no mesmo espaço de transação e não precisar se autenticar novamente.  
  
 Além disso, o uso da conexão de contexto normalmente resulta em melhor desempenho e menos uso de recurso. A conexão de contexto é uma conexão apenas em processo, portanto, ela pode contatar o servidor "diretamente", ignorando o protocolo de rede e as camadas de transporte, para enviar instruções Transact-SQL e receber resultados. O processo de autenticação é ignorado também. A figura a seguir mostra os principais componentes do **SqlClient** gerenciados provedor, bem como os diferentes componentes interagem entre si ao usar uma conexão normal e ao usar a conexão de contexto.  
  
 ![Caminhos de código de um contexto e uma conexão regular. ] (../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Caminhos de código de um contexto e uma conexão regular.")  
  
 A conexão de contexto segue um caminho de código mais curto e envolve menos componentes. Dessa forma, você pode esperar que as solicitações e os resultados sejam enviados e recebidos do servidor mais rapidamente do que em uma conexão normal. O tempo de execução da consulta no servidor é o mesmo para conexões de contexto e normais.  
  
 Há alguns casos em que você pode precisar abrir uma conexão normal separada para o mesmo servidor. Por exemplo, há algumas restrições sobre como usar a conexão de contexto, descrito em [restrições em conexões de contexto e normais](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
