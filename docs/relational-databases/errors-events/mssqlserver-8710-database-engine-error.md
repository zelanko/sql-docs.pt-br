---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b62be89caf0f916a4bfce3100f3260d31eee6bdc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653000"
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|8710|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Texto da mensagem|As funções de agregação usadas com consultas CUBE, ROLLUP ou GROUPING SET devem ser fornecidas para a mesclagem de subagregações. Para corrigir esse problema, remova a função de agregação ou grave a consulta que está usando as cláusulas UNION ALL sobre GROUP BY.|  
  
## <a name="explanation"></a>Explicação  
Uma função de agregação foi usada com CUBE, ROLLUP ou GROUPING SET e não forneceu um método para mesclar subagregações.  
  
## <a name="user-action"></a>Ação do usuário  
Para corrigir esse problema, remova a função de agregação ou grave a consulta que está usando as cláusulas UNION ALL sobre GROUP BY.  
  
