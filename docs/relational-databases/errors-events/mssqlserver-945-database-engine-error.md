---
description: MSSQLSERVER_945
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2bd18aad57eed6596ff83fc5fddbb50d33cba49a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420890"
---
# <a name="mssqlserver_945"></a>MSSQLSERVER_945
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|945|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_IS_SHUTDOWN|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser aberto devido a arquivos inacessíveis, memória ou espaço em disco insuficiente.  Consulte o log de erros do SQL Server para obter detalhes.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados não pôde ser acessado porque faltam arquivos ou outros recursos.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique o log de erros para obter informações adicionais sobre memória, espaço em disco ou falha de permissão. Confirme o local dos arquivos .mdf e .ndf do banco de dados afetado e confirme se a conta usada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] tem permissão para acessar esses arquivos. Depois de corrigir o problema, reinicialize o banco de dados usando ALTER DATABASE para defini-lo como ONLINE.  
  
