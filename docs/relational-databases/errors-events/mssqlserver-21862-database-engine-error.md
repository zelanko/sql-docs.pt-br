---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 331e07fce8dc82ee090f3e28c8281ed29514fd46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624704"
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
