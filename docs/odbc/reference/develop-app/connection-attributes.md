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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299037"
---
# <a name="connection-attributes"></a>Atributos de conexão
Atributos de conexão são características da conexão. Por exemplo, pelo fato de as transações ocorrerem no nível da conexão, o nível de isolamento da transação é um atributo de conexão. Da mesma forma, o tempo de login, ou número de segundos para esperar enquanto tenta se conectar antes de cronometrar, é um atributo de conexão.  
  
 Os atributos de conexão são definidos com **SQLSetConnectAttr** e suas configurações atuais recuperadas com **SQLGetConnectAttr**. Se **o SQLSetConnectAttr** for chamado antes de o driver ser carregado, o Driver Manager armazena os atributos em sua estrutura de conexão e os define no driver como parte do processo de conexão. Não há necessidade de que um aplicativo defina quaisquer atributos de conexão; todos os atributos de conexão têm padrões, alguns dos quais são específicos do driver.  
  
 Um atributo de conexão pode ser definido antes ou depois da conexão, ou, dependendo do atributo e do driver. O tempo de tempo de login (SQL_ATTR_LOGIN_TIMEOUT) aplica-se ao processo de conexão e só é eficaz se definido antes de conectar. Os atributos que especificam se devem usar a biblioteca do cursor ODBC (SQL_ATTR_ODBC_CURSORS) e o tamanho do pacote de rede (SQL_ATTR_PACKET_SIZE) devem ser definidos antes de se conectar, pois a biblioteca do cursor ODBC reside entre o Gerenciador de Driver e o driver e, portanto, deve ser carregada antes do driver.  
  
 Os atributos para especificar se uma fonte de dados é somente leitura ou leitura (SQL_ATTR_ACCESS_MODE) e o catálogo atual (SQL_ATTR_CURRENT_CATALOG) podem ser definidos antes ou depois da conexão, dependendo do driver. No entanto, os aplicativos interoperáveis os definem antes de se conectar, pois alguns drivers não suportam alterá-los após a conexão.  
  
 Alguns atributos de conexão têm um padrão antes da conexão ser feita, enquanto outros não. Os que fazem isso são SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Os atributos de conexão de tradução (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devem ser definidos após a conexão.  
  
 Todos os outros atributos de conexão podem ser definidos a qualquer momento. Para obter mais informações, consulte a descrição da função [SQLSetConnectAttr.](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) (Os atributos de conexão não podem ser definidos no nível do ambiente por uma chamada para **SQLSetEnvAttr**.)
