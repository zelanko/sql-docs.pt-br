---
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86dadfebb4c43ed474a033ad5100be1da86ec74c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844164"
---
# <a name="mssqlserver17194"></a>MSSQLSERVER_17194
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17194|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|O servidor não pôde carregar a biblioteca de provedores de SSL necessária para logon. A conexão foi fechada. O SSL é usado para criptografar a sequência de logon ou todas as comunicações dependendo de como o administrador configurou o servidor. Consulte Manuais Online para obter informações sobre esta mensagem de erro: 0xXXXX. [CLIENTE: 11.11.11.11]|  
  
## <a name="explanation"></a>Explicação  
Este erro indica que o cliente fechou a conexão. Este erro pode ocorrer porque o tempo limite da conexão expirou. A mensagem de erro exibe um valor do sistema operacional que descreve o problema subjacente.  
  
## <a name="user-action"></a>Ação do usuário  
Se o código de erro da mensagem for 0x2746 (valor decimal 10054), isso significa que a conexão foi redefinida pelo cliente, normalmente devido a um tempo limite. Para resolver o erro, aumente o tempo limite da conexão no cliente ou o programa de chamada.  
  
Para determinar uma solução possível para outros valores da mensagem de erro, use o comando **net helpmsg** do sistema operacional e especifique o valor decimal do código de erro.  
  
Para obter mais informações sobre como se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Configuração de rede do servidor](~/database-engine/configure-windows/server-network-configuration.md) e [Configuração de rede do cliente](~/database-engine/configure-windows/client-network-configuration.md).  
  
## <a name="internal-only"></a>Somente interno  
