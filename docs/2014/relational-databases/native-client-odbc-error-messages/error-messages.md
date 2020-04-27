---
title: Mensagens de erro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b38734544ac3accb3ddfdbcae8ae92f67b252e54
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805850"
---
# <a name="error-messages"></a>Mensagens de erro
  O texto das mensagens retornadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client é colocado no parâmetro *MessageText* de **SQLGetDiagRec**. A origem de um erro é indicada pelo cabeçalho da mensagem:  
  
 [Microsoft][ODBC Driver Manager]  
 São erros gerados pelo Gerenciador de Driver ODBC.  
  
 [Microsoft][ODBC Cursor Library]  
 São erros gerados pela biblioteca de cursores ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Esses erros são gerados pelo driver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC do Native Client. Se não houver outros nós com o nome de uma Net-Library nem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é sinal de que o erro foi encontrado no driver.  
  
 O [SQL Server Native Client] [*Net-Transportname*]  
 Esses erros são gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NET-Library, em que *net-Transportname* é o nome de exibição de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um transporte de rede do cliente (por exemplo, pipes nomeados, memória compartilhada, soquetes TCP/IP ou via). O restante da mensagem de erro contém a função Net-Library chamada e a função chamada na API de rede subjacente pela função TDS. O código de erro *pfNative* retornado com esses erros é o código de erro da pilha de protocolo de rede subjacente.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 São erros gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O restante da mensagem de erro é o texto da mensagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código *pfNative* retornado com esses erros é o número do erro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de. Para obter mais informações sobre uma lista de mensagens de erro (e seus números) que podem ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]retornados pelo, consulte as colunas descrição e erro da tabela do sistema **sysmessages** no banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dados **mestre** no.  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](handling-errors-and-messages.md)  
  
  
