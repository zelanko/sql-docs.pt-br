---
description: Configurar opções programaticamente para drivers de Arquivo de texto
title: Definindo opções programaticamente para o driver de arquivo de texto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdc130904266dcdaedf84e826d4812aa6cfbb607
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483449"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Configurar opções programaticamente para drivers de Arquivo de texto

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou equipe.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir formato|Exibe a caixa de diálogo **definir formato de texto** e permite que você especifique o esquema para tabelas individuais no diretório de fonte de dados.|Esta opção não pode ser definida dinamicamente por uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "data de contratação, histórico de salários e revisão atual de todos os funcionários".|Para definir essa opção dinamicamente, use a palavra-chave **Description** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Diretório|Seleciona o diretório de destino.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensões|Lista as extensões de nome de arquivo dos arquivos de texto na fonte de dados. Quando o driver de texto é usado, um arquivo sem extensão é criado quando a instrução de CREATE TABLE é executada com um nome que não tem extensão. Outros drivers criam um arquivo com uma extensão padrão quando nenhuma extensão é fornecida. Para criar um arquivo com uma extensão. txt, a extensão deve ser incluída no nome. Para exibir arquivos sem extensões na caixa de diálogo **definir formato de texto** , "*." deve ser adicionado à lista de extensões.|Para definir essa opção dinamicamente, use a palavra-chave **Extensions** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **ReadOnly** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Linhas a serem verificadas|O número de linhas a serem verificadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado, dado o número máximo de tipos de dados encontrados. Se forem encontrados dados que não correspondem ao tipo de dados adivinhado para a coluna, o tipo de dados será retornado como um valor nulo.<br /><br /> Para o driver de texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem verificadas; no entanto, o valor sempre usará como padrão 25. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use a palavra-chave **MAXSCANROWS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde é possível selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Ao definir um diretório de fonte de dados, especifique o diretório onde os arquivos usados com mais frequência estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório: `SELECT * FROM C:\MYDIR\EMP`<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
