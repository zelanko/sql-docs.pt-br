---
title: Atributos de Conexão | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f0fad1db10e40c71d22dd75417420c54cefa7803
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750367"
---
# <a name="connection-attributes"></a>Atributos de conexão
Atributos de Conexão são características da conexão. Por exemplo, pelo fato de as transações ocorrerem no nível da conexão, o nível de isolamento da transação é um atributo de conexão. Da mesma forma, o tempo limite de logon, ou o número de segundos de espera ao tentar se conectar antes do tempo limite, é um atributo de conexão.  
  
 Atributos de Conexão são definidos com **SQLSetConnectAttr** e suas configurações atuais são recuperadas com **SQLGetConnectAttr**. Se **SQLSetConnectAttr** é chamado antes que o driver é carregado, a Gerenciador de Driver armazena os atributos sua estrutura de conexão e define-as no driver como parte do processo de conexão. Não há nenhum requisito de que um aplicativo definir quaisquer atributos de conexão; todos os atributos de conexão têm padrões, alguns dos quais são específicos do driver.  
  
 Um atributo de conexão pode ser definido antes ou após a conexão, ou ambos, dependendo do atributo e o driver. O tempo limite de logon (SQL_ATTR_LOGIN_TIMEOUT) aplica-se ao processo de conexão e está em vigor somente se definido antes de se conectar. Os atributos que especificam se é necessário usar a biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) e o tamanho do pacote de rede (SQL_ATTR_PACKET_SIZE) devem ser definidos antes da conexão, como a biblioteca de cursores ODBC reside entre o Gerenciador de Driver e o driver e Portanto, deve ser carregado antes do driver.  
  
 Os atributos para especificar se uma fonte de dados é somente leitura ou leitura / gravação (SQL_ATTR_ACCESS_MODE) e o catálogo atual (SQL_ATTR_CURRENT_CATALOG) podem ser definidos antes ou depois de conectar-se de que, dependendo do driver. No entanto, aplicativos interoperáveis definem-las antes de se conectar porque alguns drivers não dão suporte para a alteração delas após a conexão.  
  
 Alguns atributos de conexão têm um padrão antes da conexão é feita, enquanto outros não. Os que são SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Os atributos de conexão de tradução (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devem ser definidos depois de se conectar.  
  
 Todos os outros atributos de conexão podem ser definidos a qualquer momento. Para obter mais informações, consulte o [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrição da função. (Atributos de Conexão não podem ser definidos no nível do ambiente por uma chamada para **SQLSetEnvAttr**.)
