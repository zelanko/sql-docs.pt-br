---
title: Procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 260e9a6ab31e2376132c107c19bb30b8aeee8b1c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119855"
---
# <a name="procedures"></a>Procedimentos
  Um procedimento armazenado é um objeto executável pré-compilado que contém uma ou mais instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Os procedimentos armazenados podem ter parâmetros de entrada e saída, além de gerar saída de um código de retorno de inteiro. Um aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
 Os aplicativos ODBC cujo destino é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só devem usar a execução direta para chamar um procedimento armazenado. Quando conectado a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC driver implementa [função SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360) criando um procedimento armazenado temporário, que é chamado em **SQLExecute** . Ele aumenta a sobrecarga de ter **SQLPrepare** criar um procedimento armazenado temporário que apenas chama o destino do procedimento armazenado versus diretamente o destino de executar procedimento armazenado. Mesmo quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a preparação de uma chamada exige uma viagem de ida e volta adicional na rede e a elaboração de um plano de execução que apenas chama o plano de execução de procedimento armazenado.  
  
 Os aplicativos ODBC devem usar a sintaxe de ODBC CALL ao executar um procedimento armazenado. O driver é otimizado para usar um mecanismo de chamada de procedimento remoto para chamar o procedimento quando a sintaxe de ODBC CALL é usada. Isso é mais eficiente do que o mecanismo usado para enviar uma instrução EXECUTE [!INCLUDE[tsql](../../../includes/tsql-md.md)] para o servidor.  
  
 Para obter mais informações, consulte [executando procedimentos armazenados](../../native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  