---
description: MSSQLSERVER_5237
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5333d2f1cf5da680bff3f4b2dd15b6d52c677166
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470973"
---
# <a name="mssqlserver_5237"></a>MSSQLSERVER_5237
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|5237|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Texto da mensagem|Falha na verificação entre conjuntos de linhas DBCC do objeto 'NAME' (ID de objeto O_ID) devido a um erro de consulta interno.|  
  
## <a name="explanation"></a>Explicação  
Um erro interno fez com que DBCC não conseguisse executar a consulta para verificar exibições indexadas.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando DBCC novamente.  
  
