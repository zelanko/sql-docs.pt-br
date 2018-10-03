---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 751b3615e8c54ab5899f64a6604c5a228c859879
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083806"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
    
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
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde usar o provedor criptográfico listado na mensagem de erro, porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde carregar a DLL. O nome é inválido ou a assinatura Authenticode é inválida.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se o arquivo está presente e se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissão para acessar o local. Verifique o log de erros à procura de mais mensagens relacionadas. Caso contrário, contate o provedor criptográfico para obter mais informações.  
  
  
