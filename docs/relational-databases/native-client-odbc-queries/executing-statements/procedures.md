---
title: Procedimentos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5f5e26d9616b6a0a15793463bc3e01f6fbd697f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="procedures"></a>Procedimentos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Um procedimento armazenado é um objeto executável pré-compilado que contém uma ou mais instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Os procedimentos armazenados podem ter parâmetros de entrada e saída, além de gerar saída de um código de retorno de inteiro. Um aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
 Os aplicativos ODBC cujo destino é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só devem usar a execução direta para chamar um procedimento armazenado. Quando conectado a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC driver implementa [função SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360) criando um procedimento armazenado temporário, que é chamado em **SQLExecute**. Ele aumenta a sobrecarga de ter **SQLPrepare** criar um procedimento armazenado temporário que apenas chama o destino do procedimento armazenado versus diretamente o destino de executar procedimento armazenado. Mesmo quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a preparação de uma chamada exige uma viagem de ida e volta adicional na rede e a elaboração de um plano de execução que apenas chama o plano de execução de procedimento armazenado.  
  
 Os aplicativos ODBC devem usar a sintaxe de ODBC CALL ao executar um procedimento armazenado. O driver é otimizado para usar um mecanismo de chamada de procedimento remoto para chamar o procedimento quando a sintaxe de ODBC CALL é usada. Isso é mais eficiente do que o mecanismo usado para enviar uma instrução EXECUTE [!INCLUDE[tsql](../../../includes/tsql-md.md)] para o servidor.  
  
 Para obter mais informações, consulte [executando procedimentos armazenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
