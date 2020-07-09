---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1c11ade3e23f2d520e17cdb2f981ec725633d273
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723602"
---
# <a name="mssqlserver_33027"></a>MSSQLSERVER_33027
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|33027|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto da mensagem|Falha ao carregar o provedor criptográfico '%.*ls' devido a uma assinatura inválida de Authenticode ou a um caminho de arquivo inválido. Verifique as mensagens anteriores à procura de outras falhas.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pôde usar o provedor criptográfico listado na mensagem de erro, porque o SQL Server não pôde carregar a DLL. O nome é inválido ou a assinatura Authenticode é inválida.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se o arquivo está presente e se o SQL Server tem permissão para acessar o local. Verifique o log de erros à procura de mais mensagens relacionadas. Caso contrário, contate o provedor criptográfico para obter mais informações.  
  
