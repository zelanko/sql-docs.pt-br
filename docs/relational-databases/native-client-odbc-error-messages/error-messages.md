---
title: Mensagens de erro | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d632d1d22cd8439a3d787e22301ec06ec4e0d93
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291664"
---
# <a name="error-messages"></a>Mensagens de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O texto das mensagens [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornadas pelo driver Cliente Nativo ODBC é colocado no parâmetro *MessageText* do **SQLGetDiagRec**. A origem de um erro é indicada pelo cabeçalho da mensagem:  
  
 [Microsoft][ODBC Driver Manager]  
 São erros gerados pelo Gerenciador de Driver ODBC.  
  
 [Microsoft][ODBC Cursor Library]  
 São erros gerados pela biblioteca de cursores ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Esses erros são levantados pelo driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Nativo. Se não houver outros nós com o nome de uma Net-Library nem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é sinal de que o erro foi encontrado no driver.  
  
 [Microsoft] [Cliente nativo do servidor SQL] [*Net-Transportname*]  
 Esses erros são levantados pela Biblioteca-Net, onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *net-transportname* é o nome de exibição de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporte de rede cliente (por exemplo, Chamados Pipes, Memória Compartilhada, Soquetes TCP/IP ou VIA). O restante da mensagem de erro contém a função Net-Library chamada e a função chamada na API de rede subjacente pela função TDS. O código de erro *pfNative* retornado com esses erros é o código de erro da pilha de protocolo satisfaz a rede subjacente.  
  
 [Microsoft] [Cliente nativo do servidor SQL] [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 São erros gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O restante da mensagem de erro é o texto da mensagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código *pfNative* retornado com esses [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erros é o número de erro de . Para obter mais informações sobre uma lista de mensagens de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erro (e seus números) que podem ser devolvidas por , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consulte a descrição e as colunas de erro da tabela do sistema **sysmessages** no banco de dados **mestre** em .  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
