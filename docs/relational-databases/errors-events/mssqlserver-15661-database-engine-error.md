---
description: MSSQLSERVER_15661
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f851c38ab44e84fa6afd21374c2b2d2680187a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333262"
---
# <a name="mssqlserver_15661"></a>MSSQLSERVER_15661
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|15661|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum15661|  
|Texto da mensagem|O procedimento armazenado sp_estimate_data_compression_savings não pode ser usado para tabelas temporárias.|  
  
## <a name="explanation"></a>Explicação  
Uma tabela temporária foi usada como um argumento para o procedimento armazenado sp_estimate_data_compression_savings. Embora a compactação de tabelas temporárias tenha suporte, não é possível usar sp_estimate_data_compression_savings para calcular as economias de compactação.  
  
## <a name="user-action"></a>Ação do usuário  
Remova a tabela temporária como um argumento para sp_estimate_data_compression_savings.  
  
