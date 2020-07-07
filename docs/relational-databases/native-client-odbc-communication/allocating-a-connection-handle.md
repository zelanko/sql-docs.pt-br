---
title: Alocando um identificador de conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7aee78c5b9f9b151710e3dc5feb662347b588f08
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007142"
---
# <a name="allocating-a-connection-handle"></a>Alocando um identificador de conexão
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Antes de o aplicativo poder se conectar a uma fonte de dados ou driver, ele deve alocar um identificador de conexão. Isso é feito chamando **SQLAllocHandle** com o parâmetro *HandleType* definido como SQL_HANDLE_DBC e *InputHandle* apontando para um identificador de ambiente inicializado.  
  
 As características da conexão são controladas pela definição dos atributos de conexão. Por exemplo, pelo fato de as transações ocorrerem no nível da conexão, o nível de isolamento da transação é um atributo de conexão. De modo semelhante, o tempo limite de logon, ou número de segundos para esperar durante uma tentativa de conexão antes de atingir o tempo limite, é um atributo de conexão.  
  
 Os atributos de conexão são definidos com [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), e suas configurações atuais são recuperadas com [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md). Se **SQLSetConnectAttr** for chamado antes da tentativa de conexão, o Gerenciador de driver ODBC armazenará os atributos em sua estrutura de conexão e os definirá no driver como parte do processo de conexão. Alguns atributos de conexão devem ser definidos antes da tentativa de conexão do aplicativo; outros podem ser definidos depois de estabelecida a conexão. Por exemplo, SQL_ATTR_ODBC_CURSORS deve ser definido antes de se estabelecer a conexão, mas SQL_ATTR_AUTOCOMMIT pode ser definido após o estabelecimento da conexão.  
  
 Os aplicativos executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 ou posterior, às vezes, podem melhorar seu desempenho com a redefinição do tamanho do pacote de rede de protocolo TDS (tabular data stream). O tamanho de pacote padrão é definido no servidor como 4 KB. Um tamanho de pacote de 4 KB a 8 KB geralmente oferece um desempenho melhor. Se, na prática, constatar-se que o desempenho melhora com um tamanho de pacote diferente, o aplicativo poderá redefinir o tamanho do pacote. Os aplicativos ODBC podem fazer isso antes de se conectar chamando **SQLSetConnectAttr** com a opção SQL_ATTR_PACKET_SIZE. Alguns aplicativos apresentam um desempenho melhor com um tamanho de pacote maior, mas, em geral, os aprimoramentos de desempenho são mínimos em se tratando de tamanhos de pacote maiores que 8 KB.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client tem vários atributos de conexão estendidos que um aplicativo pode usar para aumentar sua funcionalidade. Alguns desses atributos controlam as mesmas opções que podem ser especificadas em fontes de dados e usadas para substituir qualquer opção definida em uma fonte de dados. Por exemplo, se um aplicativo usa identificadores entre aspas, ele pode definir o atributo específico de driver SQL_COPT_SS_QUOTED_IDENT como SQL_QI_ON para garantir que essa opção seja sempre definida independentemente da definição de qualquer fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Comunicando-se com SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
