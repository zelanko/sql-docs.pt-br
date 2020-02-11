---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 570c0574357d9315f0e6b153f3eeabac79ec673b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63055656"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  O ODBC é uma definição padrão de uma API (interface de programação de aplicativo) usada para acessar dados em bancos de dados relacionais ou ISAM (método de acesso sequencial indexado). O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte ao ODBC por meio do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, como uma das APIs nativas para escrever aplicativos C e C++ que se comunicam com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Os programas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] escritos usando o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comunicam com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio de chamadas de função C. As versões específicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] das funções ODBC são implementadas no driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. O driver passa instruções SQL para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e retorna os resultados das instruções ao aplicativo.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client está em conformidade com a especificação do Microsoft Win32 ODBC 3.51. O driver dá suporte a aplicativos escritos usando versões anteriores do ODBC da forma definida na especificação do ODBC 3.51.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Nomes de fonte de dados e sistemas operacionais de 64 bits](data-source-names-and-64-bit-operating-systems.md)  
  
-   [Criando um aplicativo de driver ODBC do SQL Server Native Client](creating-a-driver-application.md)  
  
-   [Comunicando-se com SQL Server &#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Executando consultas &#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Processando resultados &#40;&#41;ODBC](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [Usando cursores &#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Executando transações &#40;&#41;ODBC](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [Tratando de erros e mensagens](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Executando procedimentos armazenados](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Usando funções de catálogo](using-catalog-functions.md)  
  
-   [Executando operações de cópia em massa &#40;&#41;ODBC](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Gerenciando colunas de texto e imagem](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Criando perfil de desempenho do driver ODBC](profiling-odbc-driver-performance.md)  
  
-   [Parâmetros com valor de tabela &#40;&#41;ODBC](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Melhorias de data e hora &#40;&#41;ODBC](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Tipos de CLR grandes definidos pelo usuário &#40;&#41;ODBC](large-clr-user-defined-types-odbc.md)  
  
-   [Suporte a FILESTREAM &#40;&#41;ODBC](filestream-support-odbc.md)  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Colunas esparsas dão suporte a&#41;&#40;ODBC](sparse-columns-support-odbc.md)  
  
-   [Referência de&#41; &#40;ODBC do SQL Server Native Client](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [Tópicos de instruções sobre ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação de SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Instalando o SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
