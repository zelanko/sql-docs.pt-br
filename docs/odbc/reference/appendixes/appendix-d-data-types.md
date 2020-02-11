---
title: 'Apêndice D: tipos de dados | Microsoft Docs'
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
ms.openlocfilehash: 7e709c74062e31483b042c3930572fb63ca8c786
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996204"
---
# <a name="appendix-d-data-types"></a>Apêndice D: Tipos de dados
O ODBC define dois conjuntos de tipos de dados: tipos de dados SQL e tipos de dados C. Tipos de dados SQL indicam o tipo de dados dos dados armazenados na fonte de dados. Os tipos de dados C indicam o tipo de dados dos dados armazenados em buffers de aplicativo.  
  
 Os tipos de dados SQL são definidos por cada DBMS de acordo com o padrão SQL-92. Para cada tipo de dados SQL especificado no padrão SQL-92, o ODBC define um identificador de tipo, que é um valor **#define** que é passado como um argumento em funções ODBC ou retornado nos metadados de um conjunto de resultados. Os únicos tipos de dados SQL-92 sem suporte pelo ODBC são bits (o tipo de SQL_BIT ODBC tem características diferentes), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE e NATIONAL_CHARACTER. Os drivers são responsáveis por mapear tipos de dados SQL específicos da fonte de dados para identificadores de tipo de dados SQL ODBC e identificadores de tipo de dados SQL específicos do driver. O tipo de dados SQL é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de implementação.  
  
 O ODBC define os tipos de dados C e seus identificadores de tipo ODBC correspondentes. Um aplicativo especifica o tipo de dados C do buffer que receberá dados do conjunto de resultados, passando o identificador do tipo C apropriado no argumento *TargetType* em uma chamada para **SQLBindCol** ou **SQLGetData**. Ele especifica o tipo C do buffer que contém um parâmetro de instrução passando o identificador do tipo C apropriado no argumento *ValueType* em uma chamada para **SQLBindParameter**. O tipo de dados C é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de aplicativo.  
  
> [!NOTE]  
>  Não há nenhum tipo de dados C específico do driver.  
  
 Cada tipo de dados SQL corresponde a um tipo de dados ODBC C. Antes de retornar dados da fonte de dados, o driver o converte para o tipo de dados C especificado. Antes de enviar dados para a fonte de dados, o driver o converte do tipo de dados C especificado.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Usar identificadores de tipo de dados](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [Tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [Tipos de dados do C](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [Identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Identificadores de tipo pseudo](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Transferir dados em seu formato binário](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Diretrizes para tipos de dados numéricos e de intervalo](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Converter dados de SQL para tipos de dados do C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Para obter uma explicação dos tipos de dados ODBC, consulte [tipos de dados em ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.
