---
title: Procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5bef54d188545b5e7c62d68ad889d5e3ea6ec64
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001376"
---
# <a name="procedures"></a>Procedimentos
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Um procedimento armazenado é um objeto executável pré-compilado que contém uma ou mais instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Os procedimentos armazenados podem ter parâmetros de entrada e saída, além de gerar saída de um código de retorno de inteiro. Um aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
 Os aplicativos ODBC cujo destino é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só devem usar a execução direta para chamar um procedimento armazenado. Quando conectado a versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client implementa a [função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) criando um procedimento armazenado temporário, que é então chamado em **SQLExecute**. Ele adiciona sobrecarga para que o **SQLPrepare** crie um procedimento armazenado temporário que só chame o procedimento armazenado de destino em comparação com a execução direta do procedimento armazenado de destino. Mesmo quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a preparação de uma chamada exige uma viagem de ida e volta adicional na rede e a elaboração de um plano de execução que apenas chama o plano de execução de procedimento armazenado.  
  
 Os aplicativos ODBC devem usar a sintaxe de ODBC CALL ao executar um procedimento armazenado. O driver é otimizado para usar um mecanismo de chamada de procedimento remoto para chamar o procedimento quando a sintaxe de ODBC CALL é usada. Isso é mais eficiente do que o mecanismo usado para enviar uma instrução EXECUTE [!INCLUDE[tsql](../../../includes/tsql-md.md)] para o servidor.  
  
 Para obter mais informações, consulte [executando procedimentos armazenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Executando instruções &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
