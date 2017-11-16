---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b5881b2ce3fd46c43dac7e879ce8a7aaa9b378f8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|21862|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21862|  
|Texto da mensagem|As colunas FILESTREAM não podem ser publicadas em uma publicação com o uso de um método de sincronização de 'database snapshot' nem de 'database snapshot character'.|  
  
## <a name="explanation"></a>Explicação  
Como os dados FILESTREAM não podem ser acessados por meio de um instantâneo de banco de dados, o Snapshot Agent não conseguirá ler os dados FILESTREAM quando o parâmetro *database snapshot* ou *database_snapshot_character* estiver especificado para o método de sincronização da publicação.  
  
## <a name="user-action"></a>Ação do usuário  
Altere o método de sincronização da publicação para algo diferente de *database snapshot* ou *database_snapshot_character* ou apenas exclua a coluna FILESTREAM da publicação.  
  
