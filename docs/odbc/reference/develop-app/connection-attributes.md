---
title: "Atributos de Conexão | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d62657134276621442c58639d1ef1c7f2a4b63e0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connection-attributes"></a>Atributos de conexão
Atributos de Conexão são características da conexão. Por exemplo, pelo fato de as transações ocorrerem no nível da conexão, o nível de isolamento da transação é um atributo de conexão. Da mesma forma, o tempo limite de logon, ou o número de segundos de espera durante a tentativa de conexão antes do tempo limite, é um atributo de conexão.  
  
 Atributos de Conexão são definidos com **SQLSetConnectAttr** e suas configurações atuais são recuperadas com **SQLGetConnectAttr**. Se **SQLSetConnectAttr** é chamado antes que o driver é carregado, a Gerenciador de Driver armazena os atributos sua estrutura de conexão e os definirá no driver como parte do processo de conexão. Não há nenhum requisito de que um aplicativo defina os atributos de conexão; todos os atributos de conexão têm padrões, alguns dos quais são específicos do driver.  
  
 Um atributo de conexão pode ser definido antes ou após a conexão, ou ambos, dependendo do atributo e o driver. O tempo limite de logon (SQL_ATTR_LOGIN_TIMEOUT) aplica-se ao processo de conexão e é eficaz somente se definido antes de se conectar. Os atributos que especificam se deve usar a biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) e o tamanho do pacote de rede (SQL_ATTR_PACKET_SIZE) devem ser definidos antes de se conectar, porque a biblioteca de cursores ODBC reside entre o Gerenciador de Driver e o driver e Portanto, deve ser carregado antes do driver.  
  
 Os atributos para especificar se uma fonte de dados é somente leitura ou leitura / gravação (SQL_ATTR_ACCESS_MODE) e o catálogo atual (SQL_ATTR_CURRENT_CATALOG) podem ser definidos antes ou depois de conectar-se de que, dependendo do driver. No entanto, os aplicativos interoperáveis definem-las antes de se conectar porque alguns drivers não dão suporte ao alterar esses depois de se conectar.  
  
 Alguns atributos de conexão têm um padrão antes da conexão é feita, enquanto outros não. Essas são SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Os atributos de conexão de conversão (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devem ser definidos depois de se conectar.  
  
 Todos os outros atributos de conexão podem ser definidos a qualquer momento. Para obter mais informações, consulte o [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrição da função. (Atributos de Conexão não podem ser definidos no nível do ambiente por uma chamada para **SQLSetEnvAttr**.)

