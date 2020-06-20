---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79137d0f70c05c6aa7b758f7e073d152681a14b4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054070"
---
# <a name="mssqlserver_2570"></a>MSSQLSERVER_2570
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2570|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|Texto da mensagem|Página P_ID, slot S_ID na ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE). O valor de coluna COLUMN_NAME está fora do intervalo para tipo de dados "DATATYPE". Atualize a coluna para um valor válido.|  
  
## <a name="explanation"></a>Explicação  
 O valor de coluna contido na coluna especificada está fora do intervalo de valores possíveis para o tipo de dados da coluna.  
  
## <a name="user-action"></a>Ação do usuário  
 O erro não é reparável. Atualize a coluna com um valor que esteja dentro do intervalo para o tipo de dados da coluna e execute o comando novamente.  Para obter mais informações, consulte o artigo [923247](https://support.microsoft.com/kb/923247) da Base de Dados de Conhecimento.  
  
## <a name="see-also"></a>Consulte Também  
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
