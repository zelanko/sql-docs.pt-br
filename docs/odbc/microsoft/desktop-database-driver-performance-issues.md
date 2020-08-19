---
description: Problemas de desempenho do driver de banco de dados de área de trabalho
title: Problemas de desempenho do driver de banco de dados desktop | Microsoft Docs
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
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449548"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de desempenho do driver de banco de dados de área de trabalho
Para garantir a compatibilidade com os aplicativos ANSI existentes, os tipos de dados SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR são expostos como SQL_CHAR, SQL_VARCHAR e SQL_LONGVARCHAR para fontes de dados do Microsoft Access 4,0 ou superior. As fontes de dados não retornam tipos de dados de caracteres LARGOs, mas os dados ainda devem ser enviados para o Jet no formato de caracteres largos. É importante entender que a conversão ocorrerá se um parâmetro SQL_C_CHAR ou coluna de resultado estiver associado a um tipo de dados SQL_CHAR em um aplicativo ANSI.  
  
 Essa conversão pode ser especialmente ineficiente em termos de memória quando um tipo de SQL_C_CHAR está associado a um parâmetro do tipo LONGVARCHAR. Como o mecanismo Jet 4,0 não é capaz de transmitir dados de parâmetro LONGTEXT, um buffer de conversão UNICODE deve ser alocado que é duas vezes o tamanho do buffer ANSI SQL_C_CHAR. O mecanismo mais eficiente é que o aplicativo execute a conversão UNICODE e associe o parâmetro como o tipo SQL_C_WCHAR. Quando um parâmetro é marcado como dados em execução e os dados são fornecidos em várias chamadas para SQLPutData, um buffer de dados LONGTEXT é aumentado. Uma maneira de evitar a despesa de aumentar esse buffer de "Put data" é fornecer um comprimento opcional por meio de SQL_DATA_AT_EXEC_LEN (x), em que *x* é o comprimento esperado de bytes. Isso irá inicializar o tamanho de um buffer de PutData interno para *x* bytes.  
  
> [!NOTE]  
>  Uma maneira eficiente de inserir ou atualizar dados longos pode ser realizada usando **SQLBulkOperations ()** ou **SQLSetPos ()** e definindo os dados longos como SQL_DATA_AT_EXEC. (EXEC_LEN é ignorado nesse caso.) Os dados podem ser transmitidos em partes chamando **SQLPutData** várias vezes, o que efetivamente acrescentará os dados à tabela.  
  
 Quando um aplicativo que usa um banco de dados Jet 3,5 por meio dos drivers de banco de dados Microsoft ODBC Desktop é atualizado para a versão 4,0, alguma degradação de desempenho e um maior tamanho de conjunto de trabalho podem ocorrer. Isso ocorre porque, quando uma versão 3. *x* o banco de dados é aberto usando o novo driver da versão 4,0, ele carrega o Jet 4,0. Quando o Jet 4,0 abre o banco de dados e vê que o banco de dados é um 3. *x* , ele carrega um driver ISAM instalável que é equivalente a carregar o Jet 3,5 Engine também. Para remover a penalidade de desempenho e de tamanho, o Jet 3. o banco de dados *x* deve ser compactado em um banco de dados de formato Jet 4,0. Isso eliminará o carregamento de dois mecanismos do Jet e minimizará o caminho do código para os dados.  
  
 Além disso, o mecanismo Jet 4,0 é um mecanismo Unicode. Todas as cadeias de caracteres são armazenadas e manipuladas em Unicode. Quando um aplicativo ANSI acessa um Jet 3. *x* por meio do mecanismo Jet 4,0, os dados são convertidos de ANSI para Unicode e de volta para ANSI. Se o banco de dados for atualizado para o formato de versão 4,0, as cadeias de caracteres serão convertidas em Unicode, removendo um nível de conversão de cadeia de caracteres, bem como minimizando o caminho de código para os dados, passando por apenas um mecanismo Jet.
