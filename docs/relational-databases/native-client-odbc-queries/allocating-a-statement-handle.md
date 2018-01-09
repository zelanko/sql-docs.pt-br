---
title: "Alocar um identificador de instrução | Microsoft Docs"
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
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 307e65568876acafb2d5c2936302e586fbcb1768
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para que um aplicativo possa executar uma instrução, deve alocar um identificador de instrução. Ele faz isso chamando **SQLAllocHandle** com o *HandleType* parâmetro definido como SQL_HANDLE_STMT e *InputHandle* apontando para um identificador de conexão.  
  
 Os atributos da instrução são características do identificador de instrução. O exemplo de atributos de instrução pode incluir o uso de indicadores e o tipo de cursor a ser usado com o conjunto de resultados da instrução. Atributos de instrução são definidos com [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md), e suas configurações atuais são recuperadas usando [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md). Não há nenhum requisito de que um aplicativo tenha definido qualquer atributo de instrução; todos os atributos de instrução têm padrões e alguns são específicos do driver.  
  
 Tome cuidado ao usar várias opções de conexão e instrução do ODBC. Chamando [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com *fOption* definido como controles SQL_ATTR_LOGIN_TIMEOUT a hora em que um aplicativo aguarda uma tentativa de conexão de tempo limite ao aguardar para estabelecer uma conexão (0 Especifica uma espera infinita). Os sites que têm tempos de resposta lentos podem definir este valor alto para verificar se as conexões têm tempo suficiente para serem estabelecidas. No entanto, o intervalo deve sempre ser baixo o suficiente para dar ao usuário uma resposta em um tempo razoável se o driver não puder se conectar.  
  
 Chamando **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_QUERY_TIMEOUT define um intervalo de tempo limite de consulta para ajudar a proteger o servidor e o usuário de consultas de longa execução.  
  
 Chamando **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_MAX_LENGTH limita a quantidade de **texto** e **imagem** dados que um instrução individual pode recuperar. Chamando **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_MAX_ROWS também limitará um conjunto de linhas para o primeiro  *n*  linhas se isto for todo o aplicativo requer. Observe que a configuração SQL_ATTR_MAX_ROWS faz com que o driver emita uma instrução SET ROWCOUNT ao servidor. Isso afeta todos os [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções, inclusive gatilhos e atualizações.  
  
 Tome cuidado quando você for definir estas opções. Será melhor se todos os identificações de instrução em um identificador de conexão tiverem as mesmas configurações para SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS. Se o driver alternar de um identificador de instrução para outro com valores diferentes para essas opções, o driver deverá gerar as instruções SET TEXTSIZE e SET ROWCOUNT adequadas para alterar as configurações. O driver não pode colocar essas instruções no mesmo lote que a instrução SQL do usuário, pois a instrução SQL pode conter uma instrução que deve ser a primeira instrução em um lote. O driver deve enviar as instruções SET TEXTSIZE e SET ROWCOUNT em um lote separado que automaticamente gera uma viagem de ida-e-volta adicional ao servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de consultas &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
