---
title: Problemas de desempenho do driver do banco de dados da área | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303497"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de desempenho do driver de banco de dados de área de trabalho
Para garantir a compatibilidade com os aplicativos ANSI existentes, os tipos de dados SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR são expostos como SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR para fontes de dados do Microsoft Access 4.0 ou superiores. As fontes de dados não retornam tipos de dados WIDE CHAR, mas os dados ainda devem ser enviados para a Jet em forma de Wide Char. É importante entender que a conversão ocorrerá se uma SQL_C_CHAR parâmetro ou coluna de resultados estiver vinculada a um SQL_CHAR tipo de dados em um aplicativo ANSI.  
  
 Esta conversão pode ser especialmente ineficiente em termos de memória quando um tipo de SQL_C_CHAR está vinculado a um parâmetro do tipo LONGVARCHAR. Uma vez que o mecanismo Jet 4.0 não consegue transmitir dados de parâmetros LONGTEXT, um buffer de conversão UNICODE deve ser alocado com o dobro do tamanho do buffer ANSI SQL_C_CHAR. O mecanismo mais eficiente é que a aplicação realize a conversão UNICODE e vincule o parâmetro como tipo SQL_C_WCHAR. Quando um parâmetro é marcado como data-at-execution e os dados são fornecidos em várias chamadas para SQLPutData, um buffer de dados de texto longo é cultivado. Uma maneira de evitar o gasto de crescimento deste buffer "Put Data" é fornecer um comprimento opcional via SQL_DATA_AT_EXEC_LEN(x), onde *x* é o comprimento esperado de bytes. Isso inicializará o tamanho de um buffer PutData interno para *x* bytes.  
  
> [!NOTE]  
>  Uma maneira eficiente de inserir ou atualizar dados longos pode ser realizada usando **SQLBulkOperations()** ou **SQLSetPos()** e definindo os dados longos para SQL_DATA_AT_EXEC. (EXEC_LEN é ignorada neste caso.) Os dados podem ser transmitidos em blocos ligando para **SQLPutData** várias vezes, o que efetivamente anexará os dados à tabela.  
  
 Quando um aplicativo que usa um banco de dados Jet 3.5 através do Microsoft ODBC Desktop Database Drivers é atualizado para a versão 4.0, alguma degradação de desempenho e um tamanho maior do conjunto de trabalho podem ocorrer. Isso é porque quando uma versão 3. *x* banco de dados é aberto usando o novo driver versão 4.0, ele carrega Jet 4.0. Quando o Jet 4.0 abre o banco de dados e vê que o banco de dados é um 3. *x* versão, ele carrega um driver ISAM instalável que é equivalente a carregar o motor Jet 3.5 também. Para remover o desempenho e a penalidade de tamanho, o Jet 3. *x* banco de dados deve ser compactado em um banco de dados de formato Jet 4.0. Isso eliminará o carregamento de dois motores Jet e minimizará o caminho de código para os dados.  
  
 Além disso, o motor Jet 4.0 é um motor Unicode. Todas as strings são armazenadas e manipuladas em Unicode. Quando um aplicativo ANSI acessa um Jet 3. *x* banco de dados através do mecanismo Jet 4.0, os dados são convertidos de ANSI para Unicode e de volta para ANSI. Se o banco de dados for atualizado para o formato da versão 4.0, as strings serão convertidas em Unicode, removendo um nível de conversão de strings, bem como minimizando o caminho de código para os dados, passando por apenas um motor Jet.
