---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc46a5cf1252df209243623a63ec9bdc68e71873
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131656"
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
    
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
  
  
