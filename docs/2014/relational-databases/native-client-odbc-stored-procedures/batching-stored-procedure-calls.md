---
title: Chamadas de procedimento armazenado de envio em lote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd3d7fca3dc22d20c9aeadfc3b60fa41fa64f895
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013329"
---
# <a name="batching-stored-procedure-calls"></a>Processando em lote as chamadas de procedimento armazenado
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client automaticamente processa em lotes chamadas de procedimento armazenado para o servidor quando apropriado. O driver só faz isso quando é usada a sequência de escape de ODBC CALL; não o faz para a instrução EXECUTE [!INCLUDE[tsql](../../includes/tsql-md.md)]. O processamento em lote de chamadas de procedimento armazenado pode reduzir o número de viagens de ida e volta ao servidor e aumentar significativamente o desempenho.  
  
 O driver processa em lote as chamadas de procedimento ao servidor quando você executa um lote que contém várias sequências de escape de ODBC CALL. Também processa em lote as chamadas de procedimento quando matrizes de parâmetro associadas são usadas com uma sequência de escape de ODBC CALL. Por exemplo, se você usar qualquer associação de parâmetro por linha ou ligar uma matriz com cinco elementos aos parâmetros de uma instrução SQL ODBC CALL, quando **SQLExecute** ou **SQLExecDirect** é chamado, o driver envia um único lote com cinco chamadas de procedimento para o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Executando procedimentos armazenados](running-stored-procedures.md)  
  
  