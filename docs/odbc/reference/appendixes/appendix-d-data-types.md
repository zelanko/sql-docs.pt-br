---
title: 'Apêndice d: Tipos de dados | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75ff7e83aa87bca9f33a3a8f44447af2eb60c581
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504024"
---
# <a name="appendix-d-data-types"></a>Apêndice d: Tipos de dados
ODBC define dois conjuntos de tipos de dados: Tipos de dados SQL e tipos de dados C. Tipos de dados SQL indicam o tipo de dados dos dados armazenados na fonte de dados. Tipos de dados C indicam o tipo de dados dos dados armazenados em buffers do aplicativo.  
  
 Tipos de dados SQL são definidos por cada DBMS de acordo com o padrão SQL-92. Para cada tipo de dados SQL especificado no padrão SQL-92, ODBC define um identificador de tipo, que é um **#define** valor que é passado como um argumento em funções ODBC ou retornada nos metadados de um conjunto de resultados. O SQL-92 somente tipos de dados não suportados pelo ODBC são BIT (o tipo de ODBC SQL_BIT tem características diferentes), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE e NATIONAL_CHARACTER. Drivers são responsáveis por mapeamento de tipos de dados do SQL de específico da fonte de dados para identificadores de tipo de dados SQL ODBC e identificadores de tipo de dados SQL específica do driver. O tipo de dados SQL é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de implementação.  
  
 ODBC define os tipos de dados C e seus identificadores de tipo correspondentes do ODBC. Um aplicativo especifica o tipo de dados do buffer que receberá os dados do conjunto de resultados, passando o identificador de tipo C apropriado no C a *TargetType* argumento em uma chamada para **SQLBindCol** ou  **SQLGetData**. Ela especifica o tipo de C do buffer que contém um parâmetro de instrução, passando o identificador de tipo C apropriado na *ValueType* argumento em uma chamada para **SQLBindParameter**. O tipo de dados C é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de aplicativo.  
  
> [!NOTE]  
>  Não há nenhum tipo de dados C específicos do driver.  
  
 Cada tipo de dados SQL corresponde a um tipo de dados ODBC C. Antes de retornar dados da fonte de dados, o driver converte-lo para o tipo de dados C especificado. Antes de enviar dados à fonte de dados, o driver o converte do tipo de dados C especificado.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Usando identificadores de tipo de dados](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [Tipos de dados do C](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [Identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Identificadores de tipo pseudo](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Transferindo dados em seu formato binário](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Diretrizes para tipos de dados numéricos e de intervalo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Convertendo dados de SQL para tipos de dados do C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Para obter uma explicação dos tipos de dados ODBC, consulte [tipos de dados em ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.
