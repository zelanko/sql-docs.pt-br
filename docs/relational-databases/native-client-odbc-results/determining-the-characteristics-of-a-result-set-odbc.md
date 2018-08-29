---
title: Determinando as características de um resultado definido (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0581767e2a3f93b656c4ec6ab0e971436ea4eec0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081178"
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>Determinando as características de um conjunto de resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Metadados são dados que descrevem outros dados. Por exemplo, os metadados de conjunto de resultados descrevem as características de um conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados dessas colunas, seus nomes, precisão e nulidade.  
  
 ODBC fornece metadados a aplicativos por meio de suas funções de API de catálogo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client implementa muitas das funções de catálogo de API ODBC como chamadas para um correspondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimento do catálogo.  
  
 Os aplicativos exigem metadados para a maioria das operações de conjunto de resultados. Por exemplo, o aplicativo usa o tipo de dados de uma coluna para determinar que tipo de variável associar a essa coluna. Usa o comprimento de byte de uma coluna de caractere para determinar a quantidade de espaço necessária para exibir dados dessa coluna. Como um aplicativo determina os metadados para uma coluna depende do tipo do aplicativo.  
  
 Aplicativos verticais geralmente funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Como os metadados de conjunto de resultados para esses aplicativos são definidos antes mesmo de o aplicativo ser gravado e controlado pelo desenvolvedor, eles poderão ser embutidos em código no aplicativo. Por exemplo, se uma coluna de ID de pedido for definida como um número inteiro de 4 bytes na fonte de dados, o aplicativo poderá sempre associar um número inteiro de 4 bytes a essa coluna. Quando os metadados forem embutidos em código no aplicativo, uma alteração nas tabelas usadas pelo aplicativo geralmente indica uma alteração no código do aplicativo.  
  
 Em aplicativos genéricos, principalmente aplicativos que dão suporte a consultas ad hoc, os metadados dos conjuntos de resultados que eles criam são tipicamente desconhecidos até o tempo de execução.  
  
 Para determinar as características de um conjunto de resultados, um aplicativo pode chamar:  
  
-   [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para determinar quantas colunas uma solicitação é retornada.  
  
-   [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) ou [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para descrever uma coluna no conjunto de resultados.  
  
 Um aplicativo bem projetado é gravado com a pressuposição de que o conjunto de resultados seja desconhecido e usa as informações retornadas por essas funções para associar as colunas no conjunto de resultados. Um aplicativo pode chamar essas funções a qualquer momento depois que uma instrução estiver preparada ou executada. No entanto, para otimizar o desempenho, um aplicativo deve chamar **SQLColAttribute**, **SQLDescribeCol**, e **SQLNumResultCols** depois que uma instrução é executada.  
  
 Você pode ter várias chamadas simultâneas para metadados. Os procedimentos de catálogo de sistema subjacentes às implementações de API do catálogo de ODBC podem ser chamados pelo driver ODBC enquanto estão usando cursores de servidor estáticos. Isto permite que os aplicativos processem simultaneamente várias chamadas para funções de catálogo ODBC.  
  
 Se um aplicativo utilizar um conjunto específico de metadados mais de uma vez, ele provavelmente será beneficiado pelo armazenamento em cache das informações em variáveis particulares quando for obtido pela primeira vez. Isto impede chamadas em atraso para as funções de catálogo ODBC das mesmas informações, o que força o driver a fazer viagens de ida e volta ao servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
