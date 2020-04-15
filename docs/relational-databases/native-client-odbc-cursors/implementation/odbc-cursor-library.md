---
title: Biblioteca Cursor ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93c85bc943d1a6a081cbea6bbeae40ba85aeffc5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305375"
---
# <a name="odbc-cursor-library"></a>Biblioteca de cursores ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Alguns drivers ODBC só suportam as configurações padrão do cursor; esses drivers também não suportam operações de cursor posicionadas, como **SQLSetPos**. A biblioteca de cursores ODBC é um componente do MDAC (Microsoft Data Access Components) usado para implementar cursores estáticos ou em bloco em um driver que, normalmente, não dá suporte a eles. A biblioteca do cursor também implementa instruções DE ATUALIZAÇÃO e EXCLUSão posicionadas e **SQLSetPos** para os cursores que cria.  
  
 A biblioteca de cursores ODBC é implementada como uma camada entre o Gerenciador de Driver ODBC e um driver ODBC. Se a biblioteca de cursores ODBC for carregada, o Gerenciador de Driver ODBC roteará todos os comandos relacionados com o cursor à biblioteca em vez do driver. A biblioteca de cursores implementa um cursor buscando o conjunto de resultados inteiro do driver subjacente e armazenando em cache o conjunto de resultados no cliente. Ao usar a biblioteca de cursores ODBC, o aplicativo fica limitado à funcionalidade da biblioteca; qualquer suporte adicional a outras funcionalidades de cursor no driver subjacente não estará disponível para o aplicativo.  
  
 Não há muita necessidade de usar a biblioteca de cursores ODBC com o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client porque o próprio driver dá suporte a mais funcionalidades de cursor do que a biblioteca. A única razão para usar a biblioteca [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do cursor ODBC com o driver ODBC do Cliente Nativo é porque o driver implementa seu suporte ao cursor através de cursores de servidor, e os cursores do servidor não suportam todas as instruções SQL. Sempre que houver necessidade de ter um cursor estático com procedimentos armazenados, lotes ou instruções SQL que contêm COMPUTE, COMPUTE BY, FOR BROWSE ou INTO, é recomendável usar a biblioteca de cursores ODBC. No entanto, é preciso ter cuidado ao usar a biblioteca de cursores porque ela armazena no cache do cliente o conjunto de resultados inteiro, o que pode alocar muita memória e prejudicar o desempenho.  
  
 Um aplicativo invoca a biblioteca do cursor em uma base de conexão por conexão usando [o SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para definir o atributo de conexão SQL_ATTR_ODBC_CURSORS antes de se conectar a uma fonte de dados. SQL_ATTR_ODBC_CURSORS é definido como um destes três valores:  
  
 SQL_CUR_USE_ODBC  
 Quando esta opção é [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] definida com o driver ODBC do Cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Nativo, a biblioteca do cursor ODBC substitui o suporte nativo do cursor do cliente Nativo ODBC. Somente os tipos de cursor suportados pela biblioteca de cursores podem ser usados para a conexão; cursores de servidor não podem ser usados.  
  
 SQL_CUR_USE_DRIVER  
 Quando esta opção estiver definida, todo o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte ao cursor nativo do driver ODBC do Cliente Nativo pode ser usado para a conexão. A biblioteca de cursores ODBC não pode ser usada. Todos os cursores são implementados como cursores de servidor.  
  
 SQL_CUR_USE_IF_NEEDED  
 Quando esta opção é definida, o efeito é [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o mesmo que SQL_CUR_USE_DRIVER quando usado com o driver ODBC cliente nativo. No momento da conexão, o Gerenciador de Driver oDBC testa para ver se o driver ODBC está conectado a suporte sSQL_FETCH_PRIOR opção do [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Se o driver não der suporte à opção, o Gerenciador de Driver ODBC carregará a biblioteca de cursores ODBC. Se o driver der suporte à opção, o Gerenciador não carregará a biblioteca de cursores ODBC e o aplicativo usará o suporte nativo do driver. Como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC do Cliente Nativo suporta SQL_FETCH_PRIOR, o Gerenciador de Driver ODBC não carrega a biblioteca do cursor ODBC.  
  
 A biblioteca de cursores permite que os aplicativos usem várias instruções ativas em uma conexão, assim como cursores roláveis e atualizáveis. A biblioteca de cursores deve ser carregada para dar suporte a essa funcionalidade. Use [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para especificar como a biblioteca do cursor deve ser usada e [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para especificar o tipo de cursor, a concorrência e o tamanho do conjunto de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
