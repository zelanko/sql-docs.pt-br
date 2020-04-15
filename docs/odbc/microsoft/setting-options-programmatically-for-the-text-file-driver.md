---
title: Definindo opções programáticamente para o driver de arquivo de texto | Microsoft Docs
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
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300746"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Configurar opções programaticamente para drivers de Arquivo de texto

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como Folha de Pagamento ou Pessoal.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir formato|Exibe a caixa de diálogo **Definir formato** de texto e permite especificar o esquema para tabelas individuais no diretório de origem de dados.|Essa opção não pode ser definida dinamicamente por uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "Data de contratação, histórico salarial e revisão atual de todos os funcionários."|Para definir essa opção dinamicamente, use a palavra-chave **DESCRIPTION** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Diretório|Seleciona o diretório direcionado.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensões|Lista as extensões do nome do arquivo dos arquivos de texto na fonte de dados. Quando o driver texto é usado, um arquivo sem extensão é criado quando a declaração CREATE TABLE é executada com um nome que não tem extensão. Outros drivers criam um arquivo com uma extensão padrão quando nenhuma extensão é fornecida. Para criar um arquivo com uma extensão .txt, a extensão deve ser incluída no nome. Para exibir arquivos sem extensões na caixa de diálogo Definir formato de **texto,** "*". devem ser adicionados à Lista de Extensões.|Para definir essa opção dinamicamente, use a palavra-chave **EXTENSIONS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **READONLY** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Linhas para Escanear|O número de linhas a serem verificadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado dado o número máximo de tipos de dados encontrados. Se forem encontrados dados que não correspondem ao tipo de dados adivinhado para a coluna, o tipo de dados será devolvido como um valor NULL.<br /><br /> Para o driver Texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem escaneadas; no entanto, o valor sempre será padrão para 25. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use a palavra-chave **MAXSCANROWS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório contendo os arquivos que deseja acessar.<br /><br /> Ao definir um diretório de origem de dados, especifique o diretório onde os arquivos mais usados estão localizados. O driver ODBC usa este diretório como o diretório padrão. Copie outros arquivos neste diretório se eles forem usados com freqüência. Alternativamente, você pode qualificar nomes de arquivos em uma declaração SELECT com o nome do diretório:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
