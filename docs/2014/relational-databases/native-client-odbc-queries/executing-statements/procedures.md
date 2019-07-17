---
title: Procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d030d4fb12ce9217bbdb88f501a0b0674c5a5828
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206753"
---
# <a name="procedures"></a>Procedimentos
  Um procedimento armazenado é um objeto executável pré-compilado que contém uma ou mais instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Os procedimentos armazenados podem ter parâmetros de entrada e saída, além de gerar saída de um código de retorno de inteiro. Um aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
 Os aplicativos ODBC cujo destino é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só devem usar a execução direta para chamar um procedimento armazenado. Quando conectado a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC driver implementa [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) criando um procedimento armazenado temporário, que é chamado em **SQLExecute** . Ele adiciona sobrecarga ter **SQLPrepare** criar um procedimento armazenado temporário que somente chamadas o destino de procedimento armazenado versus diretamente o destino de executar procedimento armazenado. Mesmo quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a preparação de uma chamada exige uma viagem de ida e volta adicional na rede e a elaboração de um plano de execução que apenas chama o plano de execução de procedimento armazenado.  
  
 Os aplicativos ODBC devem usar a sintaxe de ODBC CALL ao executar um procedimento armazenado. O driver é otimizado para usar um mecanismo de chamada de procedimento remoto para chamar o procedimento quando a sintaxe de ODBC CALL é usada. Isso é mais eficiente do que o mecanismo usado para enviar uma instrução EXECUTE [!INCLUDE[tsql](../../../includes/tsql-md.md)] para o servidor.  
  
 Para obter mais informações, consulte [executando procedimentos armazenados](../../native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
