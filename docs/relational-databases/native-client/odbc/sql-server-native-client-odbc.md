---
title: Cliente nativo do servidor SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 913e5387d0104fcc37c562592514801a0e2dc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303634"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O ODBC é uma definição padrão de uma API (interface de programação de aplicativo) usada para acessar dados em bancos de dados relacionais ou ISAM (método de acesso sequencial indexado). O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte ao ODBC por meio do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, como uma das APIs nativas para escrever aplicativos C e C++ que se comunicam com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Os programas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] escritos usando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comunicam com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio de chamadas de função C. As versões específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] das funções ODBC são implementadas no driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. O driver passa instruções SQL para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e retorna os resultados das instruções ao aplicativo.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client está em conformidade com a especificação do Microsoft Win32 ODBC 3.51. O driver dá suporte a aplicativos escritos usando versões anteriores do ODBC da forma definida na especificação do ODBC 3.51.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Nomes de fonte de dados e sistemas operacionais de 64 bits](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [Criando um aplicativo de driver ODBC do SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [Comunicando-se com o SQL Server &#40;o ODBC&#41;](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Execução de consultas &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Resultados de processamento &#40;&#41;Da ODBC](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [Usando cursors &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Realização de Transações &#40;&#41;Da ODBC](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
-   [Tratando de erros e mensagens](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Executando procedimentos armazenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Usando funções de catálogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [Realizando operações de cópia a granel &#40;&#41;da ODBC](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Gerenciando colunas de texto e imagem](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Criando perfil de desempenho do driver ODBC](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Melhorias de data e hora &#40;&#41;da ODBC](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [Suporte filestream &#40;o&#41;ODBC](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Suporte a colunas esparsas &#40;o&#41;da ODBC](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; Reference](https://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)  
  
-   [Tópicos de instruções sobre ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do cliente nativo do servidor SQL](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Instalando o SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
