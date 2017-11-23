---
title: Biblioteca de cursores ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9d1540cab27708bfb01cb210a2f82c771de1d57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="odbc-cursor-library"></a>Biblioteca de cursores ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Alguns drivers ODBC só oferece suporte às configurações de cursor padrão; Esses drivers também não dão suporte a operações de cursor posicionadas, como **SQLSetPos**. A biblioteca de cursores ODBC é um componente do MDAC (Microsoft Data Access Components) usado para implementar cursores estáticos ou em bloco em um driver que, normalmente, não dá suporte a eles. A biblioteca de cursores também implementa instruções UPDATE e DELETE posicionadas e **SQLSetPos** para os cursores que ele cria.  
  
 A biblioteca de cursores ODBC é implementada como uma camada entre o Gerenciador de Driver ODBC e um driver ODBC. Se a biblioteca de cursores ODBC for carregada, o Gerenciador de Driver ODBC roteará todos os comandos relacionados com o cursor à biblioteca em vez do driver. A biblioteca de cursores implementa um cursor buscando o conjunto de resultados inteiro do driver subjacente e armazenando em cache o conjunto de resultados no cliente. Ao usar a biblioteca de cursores ODBC, o aplicativo fica limitado à funcionalidade da biblioteca; qualquer suporte adicional a outras funcionalidades de cursor no driver subjacente não estará disponível para o aplicativo.  
  
 Não há muita necessidade de usar a biblioteca de cursores ODBC com o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client porque o próprio driver dá suporte a mais funcionalidades de cursor do que a biblioteca. A única razão para usar a biblioteca de cursores ODBC com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client é porque o driver implementa seu suporte de cursor por meio de cursores de servidor e cursores de servidor não oferecem suporte a todas as instruções SQL. Sempre que houver necessidade de ter um cursor estático com procedimentos armazenados, lotes ou instruções SQL que contêm COMPUTE, COMPUTE BY, FOR BROWSE ou INTO, é recomendável usar a biblioteca de cursores ODBC. No entanto, é preciso ter cuidado ao usar a biblioteca de cursores porque ela armazena no cache do cliente o conjunto de resultados inteiro, o que pode alocar muita memória e prejudicar o desempenho.  
  
 Um aplicativo invoca a biblioteca de cursores em uma base de conexão por conexão usando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para definir o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar a uma fonte de dados. SQL_ATTR_ODBC_CURSORS é definido como um destes três valores:  
  
 SQL_CUR_USE_ODBC  
 Quando essa opção é definida com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC Native Client, a biblioteca de cursores ODBC substitui o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o suporte nativo do cursor do driver ODBC Native Client. Somente os tipos de cursor suportados pela biblioteca de cursores podem ser usados para a conexão; cursores de servidor não podem ser usados.  
  
 SQL_CUR_USE_DRIVER  
 Quando essa opção for definida, todos do cursor oferecem suporte nativo para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client pode ser usado para a conexão. A biblioteca de cursores ODBC não pode ser usada. Todos os cursores são implementados como cursores de servidor.  
  
 SQL_CUR_USE_IF_NEEDED  
 Quando essa opção for definida, o efeito é o mesmo que SQL_CUR_USE_DRIVER quando usada com a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. No momento da conexão, o Gerenciador de Driver ODBC verifica se o driver ODBC que está sendo conectado ao dá suporte à opção SQL_FETCH_PRIOR de [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Se o driver não der suporte à opção, o Gerenciador de Driver ODBC carregará a biblioteca de cursores ODBC. Se o driver der suporte à opção, o Gerenciador não carregará a biblioteca de cursores ODBC e o aplicativo usará o suporte nativo do driver. Porque o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a SQL_FETCH_PRIOR, o Gerenciador de Driver ODBC não carregar a biblioteca de cursores ODBC.  
  
 A biblioteca de cursores permite que os aplicativos usem várias instruções ativas em uma conexão, assim como cursores roláveis e atualizáveis. A biblioteca de cursores deve ser carregada para dar suporte a essa funcionalidade. Use [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para especificar como a biblioteca de cursores deve ser usada e [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para especificar o tamanho de tipo, simultaneidade e conjunto de linhas do cursor.  
  
## <a name="see-also"></a>Consulte também  
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
