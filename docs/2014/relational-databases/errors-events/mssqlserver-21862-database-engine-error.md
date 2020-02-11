---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f336c64ffc0d044fa0f7282f3c87451483353879
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914946"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|MSSQLSERVER|  
|ID do evento|21862|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21862|  
|Texto da mensagem|As colunas FILESTREAM não podem ser publicadas em uma publicação com o uso de um método de sincronização de 'database snapshot' nem de 'database snapshot character'.|  
  
## <a name="explanation"></a>Explicação  
 Como os dados FILESTREAM não podem ser acessados por meio de um instantâneo de banco de dados, o Snapshot Agent não conseguirá ler os dados FILESTREAM quando o parâmetro *database snapshot* ou *database_snapshot_character* estiver especificado para o método de sincronização da publicação.  
  
## <a name="user-action"></a>Ação do usuário  
 Altere o método de sincronização da publicação para algo diferente de *database snapshot* ou *database_snapshot_character* ou apenas exclua a coluna FILESTREAM da publicação.  
  
  
