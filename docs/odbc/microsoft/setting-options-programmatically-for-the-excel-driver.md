---
title: Configurando opções programaticamente para o Driver do Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47181fca07aff7b2a0d418b8852cfce47cf9e501
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063520"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Configurar opções programaticamente para drivers do Excel

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou pessoal.|Para definir essa opção dinamicamente, use o **DSN** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados é fornecido após a instalação, o usuário será solicitado para escolher um arquivo de banco de dados ao conectar-se à fonte de dados.|Para definir essa opção dinamicamente, use o **DBQ** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Diretório|Exibe o diretório selecionado no momento.<br /><br /> Para arquivos do Microsoft Excel 3.0/4.0, a exibição do caminho é rotulado como "Directory", e para o Microsoft Excel 5.0, 7.0 ou 97 arquivos, a exibição do caminho é rotulado como "Pasta de trabalho".|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Linhas de varredura|O número de linhas a serem examinadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado, considerando o número máximo de tipos de dados encontrados. Se forem encontrados dados que não coincide com o tipo de dados avaliado para a coluna, o tipo de dados será retornado como um valor nulo.<br /><br /> Para o driver do Microsoft Excel, você pode inserir um número de 1 a 16 para as linhas a serem examinadas. O valor padrão é 8; Se ele for definido como 0, todas as linhas são verificadas. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use o **MAXSCANROWS** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Ao definir um diretório de origem de dados (para todos os drivers, exceto o Microsoft Access), especifique o diretório onde seus arquivos mais comumente usados estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório, se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONE \* DE C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando o **SQLSetConnectOption** função com a opção SQL_CURRENT_QUALIFIER.<br /><br /> Para o Microsoft Excel 3.0 ou 4.0 arquivos, a exibição do caminho é rotulado como "Directory" e o botão de seleção de caminho é rotulado como "Selecionar diretório". Para arquivos do Microsoft Excel 97, 7.0 ou 5.0, a exibição do caminho é rotulado como "Pasta de trabalho" e o botão de seleção de caminho é rotulado como "Selecione a pasta de trabalho". Ao definir um diretório de origem de dados, especifique o diretório onde os arquivos do Microsoft Excel mais comumente usados estão localizados para o Microsoft Excel 3.0/4.0 ou o diretório onde o arquivo de pasta de trabalho está localizado para o Microsoft Excel 97, 7.0 ou 5.0. **Usar o diretório atual** está desabilitado para o Microsoft Excel 97, 7.0 e 5.0.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
