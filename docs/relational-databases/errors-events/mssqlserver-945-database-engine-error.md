---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1670253eab7d92b07d8b5c1681d82c497be483e6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326347"
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|945|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_IS_SHUTDOWN|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser aberto devido a arquivos inacessíveis, memória ou espaço em disco insuficiente.  Consulte o log de erros do SQL Server para obter detalhes.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados não pôde ser acessado porque faltam arquivos ou outros recursos.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique o log de erros para obter informações adicionais sobre memória, espaço em disco ou falha de permissão. Confirme o local dos arquivos .mdf e .ndf do banco de dados afetado e confirme se a conta usada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] tem permissão para acessar esses arquivos. Depois de corrigir o problema, reinicialize o banco de dados usando ALTER DATABASE para defini-lo como ONLINE.  
  
