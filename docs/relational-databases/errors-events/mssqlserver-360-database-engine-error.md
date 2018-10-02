---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e250985c9f1dc2ed043c55d9182b932e00dc1365
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832801"
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|360|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DML_UPDATE_SPARSE_AND_COLSET|  
|Texto da mensagem|A lista de colunas de destino de uma instrução INSERT, UPDATE ou MERGE não pode conter uma coluna esparsa e o conjunto de colunas que contém a coluna esparsa. Reescreva a instrução para incluir a coluna esparsa ou o conjunto de colunas, mas não ambos.|  
  
## <a name="explanation"></a>Explicação  
Um conjunto de colunas é uma representação em XML sem-tipo que combina algumas colunas de uma tabela em uma saída estruturada. Foi realizada uma tentativa para modificar o conjunto de colunas e a coluna incluída no conjunto de colunas, gerando duas referências para a mesma coluna.  
  
## <a name="user-action"></a>Ação do usuário  
Reescreva a instrução para incluir referências à coluna esparsa ou ao conjunto de colunas, mas não inclua ambos na instrução.  
  
