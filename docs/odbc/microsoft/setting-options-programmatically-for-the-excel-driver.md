---
title: Definindo opções programáticas para o Driver Excel | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300766"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Configurar opções programaticamente para drivers do Excel

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como Folha de Pagamento ou Pessoal.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados for fornecido após a configuração, o usuário será solicitado a escolher um arquivo de banco de dados ao se conectar à fonte de dados.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "Data de contratação, histórico salarial e revisão atual de todos os funcionários."|Para definir essa opção dinamicamente, use a palavra-chave **DESCRIPTION** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Diretório|Exibe o diretório selecionado no momento.<br /><br /> Para os arquivos Microsoft Excel 3.0/4.0, a exibição do caminho é rotulada como "Diretório", enquanto para os arquivos Microsoft Excel 5.0, 7.0 ou 97, a exibição do caminho é rotulada como "Pasta de Trabalho".|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **READONLY** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Linhas para Escanear|O número de linhas a serem verificadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado dado o número máximo de tipos de dados encontrados. Se forem encontrados dados que não correspondem ao tipo de dados adivinhado para a coluna, o tipo de dados será devolvido como um valor NULL.<br /><br /> Para o driver microsoft excel, você pode inserir um número de 1 a 16 para que as linhas escaneiem. O valor é padrão para 8; se for definido como 0, todas as linhas são digitalizadas. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use a palavra-chave **MAXSCANROWS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório contendo os arquivos que deseja acessar.<br /><br /> Ao definir um diretório de origem de dados (para todos os drivers, exceto o Microsoft Access), especifique o diretório onde seus arquivos mais usados estão localizados. O driver ODBC usa este diretório como o diretório padrão. Copie outros arquivos neste diretório se eles forem usados com freqüência. Alternativamente, você pode qualificar nomes de arquivos em uma declaração SELECT com o nome do diretório:<br /><br /> SELECIONE \* C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.<br /><br /> Para os arquivos Microsoft Excel 3.0 ou 4.0, a exibição do caminho é rotulada como "Diretório", e o botão de seleção de caminho seleção é rotulado como "Select Directory". Para os arquivos Microsoft Excel 5.0, 7.0 ou 97, a exibição do caminho é rotulada como "Pasta de trabalho", e o botão de seleção de caminho seleção é rotulado como "Selecionar Pasta de Trabalho". Ao definir um diretório de origem de dados, especifique o diretório onde os arquivos Microsoft Excel mais usados estão localizados para o Microsoft Excel 3.0/4.0 ou o diretório onde o arquivo da pasta de trabalho está localizado para o Microsoft Excel 5.0, 7.0 ou 97. **O diretório atual** está desativado para o Microsoft Excel 5.0, 7.0 e 97.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
