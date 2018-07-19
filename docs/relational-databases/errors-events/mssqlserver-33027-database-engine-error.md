---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d9b03347fb6ca83827854f4af0b75e8accc131
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190946"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|33027|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto da mensagem|Falha ao carregar o provedor criptográfico '%.*ls' devido a uma assinatura inválida de Authenticode ou a um caminho de arquivo inválido. Verifique as mensagens anteriores à procura de outras falhas.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pôde usar o provedor criptográfico listado na mensagem de erro, porque o SQL Server não pôde carregar a DLL. O nome é inválido ou a assinatura Authenticode é inválida.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se o arquivo está presente e se o SQL Server tem permissão para acessar o local. Verifique o log de erros à procura de mais mensagens relacionadas. Caso contrário, contate o provedor criptográfico para obter mais informações.  
  
