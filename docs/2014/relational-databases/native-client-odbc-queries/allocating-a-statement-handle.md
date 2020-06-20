---
title: Alocando um identificador de instrução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fac0802b474f38f6a6c314dd727fa335d14598d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018699"
---
# <a name="allocating-a-statement-handle"></a>Alocando um identificador de instrução
  Para que um aplicativo possa executar uma instrução, deve alocar um identificador de instrução. Ele faz isso chamando **SQLAllocHandle** com o parâmetro *HandleType* definido como SQL_HANDLE_STMT e *InputHandle* apontando para um identificador de conexão.  
  
 Os atributos da instrução são características do identificador de instrução. O exemplo de atributos de instrução pode incluir o uso de indicadores e o tipo de cursor a ser usado com o conjunto de resultados da instrução. Os atributos de instrução são definidos com [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md), e suas configurações atuais são recuperadas usando [SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md). Não há nenhum requisito de que um aplicativo tenha definido qualquer atributo de instrução; todos os atributos de instrução têm padrões e alguns são específicos do driver.  
  
 Tome cuidado ao usar várias opções de conexão e instrução do ODBC. Chamar [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) com *fOption* definido como SQL_ATTR_LOGIN_TIMEOUT controla a hora em que um aplicativo aguarda uma tentativa de conexão atingir o tempo limite enquanto aguarda para estabelecer uma conexão (0 especifica uma espera infinita). Os sites que têm tempos de resposta lentos podem definir este valor alto para verificar se as conexões têm tempo suficiente para serem estabelecidas. No entanto, o intervalo deve sempre ser baixo o suficiente para dar ao usuário uma resposta em um tempo razoável se o driver não puder se conectar.  
  
 Chamar **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_QUERY_TIMEOUT define um intervalo de tempo limite de consulta para ajudar a proteger o servidor e o usuário de consultas de longa execução.  
  
 Chamar **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_MAX_LENGTH limita a quantidade de dados de **texto** e **imagem** que uma instrução individual pode recuperar. Chamar **SQLSetStmtAttr** com *fOption* definido como SQL_ATTR_MAX_ROWS também limita um conjunto de linhas às primeiras *n* linhas se isso for todo o aplicativo exigir. Observe que a configuração SQL_ATTR_MAX_ROWS faz com que o driver emita uma instrução SET ROWCOUNT ao servidor. Isso afeta todas as [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções, incluindo gatilhos e atualizações.  
  
 Tome cuidado quando você for definir estas opções. Será melhor se todos os identificações de instrução em um identificador de conexão tiverem as mesmas configurações para SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS. Se o driver alternar de um identificador de instrução para outro com valores diferentes para essas opções, o driver deverá gerar as instruções SET TEXTSIZE e SET ROWCOUNT adequadas para alterar as configurações. O driver não pode colocar essas instruções no mesmo lote que a instrução SQL do usuário, pois a instrução SQL pode conter uma instrução que deve ser a primeira instrução em um lote. O driver deve enviar as instruções SET TEXTSIZE e SET ROWCOUNT em um lote separado que automaticamente gera uma viagem de ida-e-volta adicional ao servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
