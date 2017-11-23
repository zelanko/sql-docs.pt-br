---
title: "Problemas de desempenho do Driver de banco de dados de área de trabalho | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: beb888ab7920bdac942c60d26980a71a34a54800
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de desempenho do Driver de banco de dados de área de trabalho
Para garantir a compatibilidade com aplicativos existentes de ANSI, os tipos de dados SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR são expostos como SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR para Microsoft Access 4.0 ou mais fontes de dados. As fontes de dados não retornam tipos de dados CHAR grande, mas os dados ainda devem ser enviados para Jet no formulário Char ampla. É importante entender que conversão ocorrerá se uma coluna de parâmetro ou o resultado SQL_C_CHAR estiver associada a um tipo de dados SQL_CHAR em um aplicativo de ANSI.  
  
 Esta conversão pode ser especialmente ineficiente em termos de memória quando um tipo SQL_C_CHAR é associado a um parâmetro do tipo LONGVARCHAR. Como o mecanismo Jet 4.0 é incapaz de fluxo de dados do parâmetro LONGTEXT, um buffer de conversão UNICODE deve ser duas vezes o tamanho do buffer SQL_C_CHAR de ANSI alocado. É o mecanismo mais eficiente para o aplicativo executar a conversão de UNICODE e associar o parâmetro como tipo SQL_C_WCHAR. Quando um parâmetro está marcado como dados em execução e os dados são fornecidos em várias chamadas para SQLPutData, um buffer de dados longtext é crescer. Uma maneira de evitar a despesa de crescimento isso buffer "Colocar dados" é fornecer um comprimento opcional via SQL_DATA_AT_EXEC_LEN(x), onde *x* é o tamanho esperado de bytes. Isso inicializará o tamanho de um buffer interno PutData *x* bytes.  
  
> [!NOTE]  
>  Uma maneira eficiente de inserir ou atualizar dados longos pode ser realizada usando **SQLBulkOperations()** ou **SQLSetPos()** e definindo os dados longos como SQL_DATA_AT_EXEC. (EXEC_LEN é ignorado nesse caso.) Dados podem ser transmitidos em partes chamando **SQLPutData** várias vezes, que efetivamente adicionará os dados à tabela.  
  
 Quando um aplicativo usando um banco de dados Jet 3.5 por meio de Drivers de banco de dados do Microsoft ODBC Desktop é atualizado para a versão 4.0, podem ocorrer degradação no desempenho e um maior tamanho de conjunto de trabalho. Isso ocorre porque quando uma versão 3. *x* banco de dados é aberto usando a versão 4.0 do driver novo, ele carrega o Jet 4.0. Quando o Jet 4.0 abre o banco de dados e vê que o banco de dados é um 3. *x* versão, ele carrega um driver de ISAM instalável é equivalente ao carregar o mecanismo Jet 3.5. Para remover a penalidade de desempenho e tamanho, o Jet 3. *x* banco de dados deve ser compactado em um banco de dados de formato do Jet 4.0. Isso eliminar carregar dois mecanismos de Jet e minimizar o caminho de código para os dados.  
  
 Além disso, o mecanismo Jet 4.0 é um mecanismo de Unicode. Todas as cadeias de caracteres são armazenadas e manipuladas em Unicode. Quando um aplicativo ANSI acessa um Jet 3. *x* banco de dados por meio do mecanismo Jet 4.0, os dados é convertido de ANSI em Unicode e de volta para ANSI. Se o banco de dados é atualizado para o formato da versão 4.0, as cadeias de caracteres são convertidas para Unicode, remover um nível de conversão de cadeia de caracteres, bem como minimizar o caminho de código para os dados por meio de apenas um mecanismo Jet.
