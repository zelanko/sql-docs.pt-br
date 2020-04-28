---
title: Definindo opções programaticamente para o driver do Excel | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300766"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Configurar opções programaticamente para drivers do Excel

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou equipe.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dado. Se nenhum banco de dados for fornecido na instalação, será solicitado que o usuário escolha um arquivo de banco de dados ao conectar-se à fonte.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "data de contratação, histórico de salários e revisão atual de todos os funcionários".|Para definir essa opção dinamicamente, use a palavra-chave **Description** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Diretório|Exibe o diretório selecionado no momento.<br /><br /> Para arquivos do Microsoft Excel 3.0/4.0, a exibição do caminho é rotulada "diretório", enquanto para arquivos do Microsoft Excel 5,0, 7,0 ou 97, a exibição do caminho é rotulada "pasta de trabalho".|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **ReadOnly** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Linhas a serem verificadas|O número de linhas a serem verificadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado, dado o número máximo de tipos de dados encontrados. Se forem encontrados dados que não correspondem ao tipo de dados adivinhado para a coluna, o tipo de dados será retornado como um valor nulo.<br /><br /> Para o driver do Microsoft Excel, você pode inserir um número de 1 a 16 para as linhas a serem verificadas. O valor padrão é 8; Se for definido como 0, todas as linhas serão verificadas. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use a palavra-chave **MAXSCANROWS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde é possível selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Ao definir um diretório de fonte de dados (para todos os drivers, exceto Microsoft Access), especifique o diretório onde os arquivos usados com mais frequência estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONAR \* de C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.<br /><br /> Para arquivos do Microsoft Excel 3,0 ou 4,0, a exibição do caminho é rotulada "diretório" e o botão de seleção de caminho é rotulado como "Selecionar diretório". Para arquivos do Microsoft Excel 5,0, 7,0 ou 97, a exibição do caminho é rotulada como "pasta de trabalho" e o botão de seleção de caminho é rotulado como "Selecionar pasta de trabalho". Ao definir um diretório de fonte de dados, especifique o diretório em que os arquivos do Microsoft Excel usados com mais frequência estão localizados para o Microsoft Excel 3.0/4.0 ou o diretório em que o arquivo de pasta de trabalho está localizado para o Microsoft Excel 5,0, 7,0 ou 97. **Usar o diretório atual** está desabilitado para o Microsoft Excel 5,0, 7,0 e 97.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
