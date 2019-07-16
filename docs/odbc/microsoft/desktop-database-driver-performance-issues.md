---
title: Problemas de desempenho do Driver de banco de dados da área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 660b7c123d0ddd0a3f1b972fa3b1dc153b15ed50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071928"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de desempenho do driver de banco de dados de área de trabalho
Para garantir a compatibilidade com aplicativos existentes de ANSI, os tipos de dados SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR são expostos como SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR para Microsoft Access 4.0 ou superiores fontes de dados. As fontes de dados não retornam tipos de dados de CARACTERE LARGO, mas os dados ainda devem ser enviados para Jet no formato de caractere largo. É importante entender que conversão acontecerá se uma coluna de parâmetro ou o resultado SQL_C_CHAR estiver associada a um tipo de dados SQL_CHAR em um aplicativo ANSI.  
  
 Essa conversão pode ser especialmente ineficiente em termos de memória quando um tipo SQL_C_CHAR é associado a um parâmetro de tipo LONGVARCHAR. Uma vez que o mecanismo Jet 4.0 é incapaz de fluxo de dados de parâmetro LONGTEXT, um buffer de conversão de UNICODE deve ser duas vezes o tamanho do buffer SQL_C_CHAR de ANSI alocado. É o mecanismo mais eficiente para o aplicativo realizar a conversão de UNICODE e associar o parâmetro como SQL_C_WCHAR de tipo. Quando um parâmetro está marcado como dados em execução e os dados são fornecidos em várias chamadas para o SQLPutData, um buffer de dados longtext é crescer. Uma maneira para evitar a despesa de crescimento isso buffer "Colocar dados" é fornecer um comprimento opcional via SQL_DATA_AT_EXEC_LEN(x), onde *x* é o tamanho esperado de bytes. Isso inicializará o tamanho de um buffer interno de PutData para *x* bytes.  
  
> [!NOTE]  
>  Uma maneira eficiente de inserção ou atualização de dados longo pode ser feita usando **SQLBulkOperations()** ou **SQLSetPos()** e definindo os dados longos como SQL_DATA_AT_EXEC. (EXEC_LEN é ignorado nesse caso.) Dados podem ser transmitidos em partes, chamando **SQLPutData** várias vezes, que efetivamente acrescentará os dados na tabela.  
  
 Quando um aplicativo usando um banco de dados Jet 3.5 por meio de Drivers de banco de dados do Microsoft ODBC Desktop é atualizado para a versão 4.0, podem ocorrer alguma degradação no desempenho e um maior tamanho de conjunto de trabalho. Isso ocorre porque quando uma versão 3. *x* banco de dados é aberto usando o novo driver de versão 4.0, ele carrega o Jet 4.0. Quando o Jet 4.0 abre o banco de dados e vê que o banco de dados é um 3. *x* versão, ele carrega um driver ISAM instalável que é equivalente a carregar o mecanismo Jet 3.5. Para remover a penalidade de desempenho e tamanho, o Jet 3. *x* banco de dados deve ser compactado em um banco de dados de formato de Jet 4.0. Isso elimina o Carregando dois motores a jato e minimizar o caminho de código para os dados.  
  
 Além disso, o mecanismo Jet 4.0 é um mecanismo de Unicode. Todas as cadeias de caracteres são armazenadas e manipuladas em Unicode. Quando um aplicativo ANSI acessa um Jet 3. *x* banco de dados por meio do mecanismo Jet 4.0, os dados é convertido de ANSI em Unicode e de volta para ANSI. Se o banco de dados é atualizado para o formato da versão 4.0, as cadeias de caracteres são convertidas para Unicode, remover um nível de conversão de cadeia de caracteres, bem como a minimizar o caminho de código para os dados por meio de apenas um mecanismo Jet.
