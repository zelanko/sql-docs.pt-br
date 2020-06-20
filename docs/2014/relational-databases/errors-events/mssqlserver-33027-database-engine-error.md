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
ms.openlocfilehash: f6bb461b42b66368224fffd2c14f9b4da61abf5b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033859"
---
# <a name="mssqlserver_33027"></a>MSSQLSERVER_33027
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|33027|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto da mensagem|Falha ao carregar o provedor criptográfico '%.*ls' devido a uma assinatura inválida de Authenticode ou a um caminho de arquivo inválido. Verifique as mensagens anteriores à procura de outras falhas.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde usar o provedor criptográfico listado na mensagem de erro, porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde carregar a DLL. O nome é inválido ou a assinatura Authenticode é inválida.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se o arquivo está presente e se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissão para acessar o local. Verifique o log de erros à procura de mais mensagens relacionadas. Caso contrário, contate o provedor criptográfico para obter mais informações.  
  
  
