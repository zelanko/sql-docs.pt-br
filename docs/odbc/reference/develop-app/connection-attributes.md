---
title: Atributos de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09b29277d74383abff1510ca7394aecad036fc7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036443"
---
# <a name="connection-attributes"></a>Atributos de conexão
Os atributos de conexão são características da conexão. Por exemplo, pelo fato de as transações ocorrerem no nível da conexão, o nível de isolamento da transação é um atributo de conexão. Da mesma forma, o tempo limite de logon ou o número de segundos a aguardar durante a tentativa de conexão antes do tempo limite é um atributo de conexão.  
  
 Os atributos de conexão são definidos com **SQLSetConnectAttr** e suas configurações atuais recuperadas com **SQLGetConnectAttr**. Se **SQLSetConnectAttr** for chamado antes de o driver ser carregado, o Gerenciador de driver armazenará os atributos em sua estrutura de conexão e os definirá no driver como parte do processo de conexão. Não há nenhum requisito de que um aplicativo defina qualquer atributo de conexão; todos os atributos de conexão têm padrões, alguns dos quais são específicos do driver.  
  
 Um atributo de conexão pode ser definido antes ou depois da conexão, ou qualquer, dependendo do atributo e do driver. O tempo limite de logon (SQL_ATTR_LOGIN_TIMEOUT) se aplica ao processo de conexão e só é eficaz se definido antes da conexão. Os atributos que especificam se a biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) deve ser usada e o tamanho do pacote de rede (SQL_ATTR_PACKET_SIZE) devem ser definidos antes da conexão, pois a biblioteca de cursores ODBC reside entre o Gerenciador de driver e o driver e Portanto, deve ser carregado antes do driver.  
  
 Os atributos para especificar se uma fonte de dados é somente leitura ou de leitura/gravação (SQL_ATTR_ACCESS_MODE) e se o catálogo atual (SQL_ATTR_CURRENT_CATALOG) pode ser definido antes ou depois da conexão, dependendo do driver. No entanto, os aplicativos interoperáveis os definem antes de se conectar, pois alguns drivers não dão suporte à alteração deles após a conexão.  
  
 Alguns atributos de conexão têm um padrão antes que a conexão seja feita, enquanto outros não. Os que são SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Os atributos de conexão de tradução (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devem ser definidos após a conexão.  
  
 Todos os outros atributos de conexão podem ser definidos a qualquer momento. Para obter mais informações, consulte a descrição da função [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) . (Os atributos de conexão não podem ser definidos no nível de ambiente por uma chamada para **SQLSetEnvAttr**.)
