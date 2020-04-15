---
title: 'Apêndice D: Tipos de Dados | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292456"
---
# <a name="appendix-d-data-types"></a>Apêndice D: Tipos de dados
O ODBC define dois conjuntos de tipos de dados: tipos de dados SQL e tipos de dados C. Os tipos de dados SQL indicam o tipo de dados armazenados na fonte de dados. Os tipos de dados C indicam o tipo de dados armazenados em buffers de aplicativos.  
  
 Os tipos de dados SQL são definidos por cada DBMS de acordo com a norma SQL-92. Para cada tipo de dados SQL especificado na norma SQL-92, o ODBC define um identificador de tipo, que é um valor **#define** que é passado como um argumento nas funções ODBC ou retornado nos metadados de um conjunto de resultados. Os únicos tipos de dados SQL-92 não suportados pelo ODBC são BIT (o tipo de SQL_BIT ODBC tem características diferentes), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE e NATIONAL_CHARACTER. Os drivers são responsáveis por mapear os tipos de dados SQL específicos da fonte de dados para identificadores de tipo de dados SQL do ODBC e identificadores de tipo SQL específicos para driver. O tipo de dados SQL é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de implementação.  
  
 O ODBC define os tipos de dados C e seus identificadores de tipo ODBC correspondentes. Um aplicativo especifica o tipo de dados C do buffer que receberá dados definidos por resultados, passando o identificador de tipo C apropriado no argumento *TargetType* em uma chamada para **SQLBindCol** ou **SQLGetData**. Ele especifica o tipo C do buffer contendo um parâmetro de declaração, passando o identificador de tipo C apropriado no argumento *ValueType* em uma chamada para **SQLBindParameter**. O tipo de dados C é especificado no campo SQL_DESC_CONCISE_TYPE de um descritor de aplicativo.  
  
> [!NOTE]  
>  Não há tipos de dados C específicos para driver.  
  
 Cada tipo de dados SQL corresponde a um tipo de dados ODBC C. Antes de retornar os dados da fonte de dados, o driver converte-os para o tipo de dados C especificado. Antes de enviar dados para a fonte de dados, o driver converte-os do tipo de dados C especificado.  
  
 Este apêndice contém os seguintes tópicos.  
  
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
  
 Para obter uma explicação dos tipos de dados da ODBC, consulte [Tipos de dados no ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.
