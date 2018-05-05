---
title: Definindo opções de forma programática para o Driver dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcff8e5aefcd3ea810aae31d933cad14bc7541ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Definindo opções de forma programática para o Driver dBASE
|Opção|Description|Método|  
|------------|-----------------|------------|  
|Número aproximado de linhas|Determina se as estatísticas de tamanho de tabela são aproximadas. Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.|Para definir essa opção dinamicamente, use o **estatísticas** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sequência de agrupamento|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou internacional.|Para definir essa opção dinamicamente, use o **COLLATINGSEQUENCE** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou pessoal.|Para definir essa opção dinamicamente, use o **DSN** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados é fornecido após a instalação, os usuários serão solicitados a selecionar um arquivo de banco de dados ao conectar-se à fonte de dados.|Para definir essa opção dinamicamente, use o **DBQ** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Description|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusive|Se o **exclusivo** caixa é selecionada, o banco de dados será aberto no modo exclusivo e pode ser acessado somente por um usuário por vez. O desempenho é melhorado quando ele é executado no modo exclusivo.|Para definir essa opção dinamicamente, use o **exclusivo** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tempo limite da página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de ser removido. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo se a opção de tempo limite de página está definida abaixo do valor.|Para definir essa opção dinamicamente, use o **PAGETIMEOUT** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Selecione o diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Quando você define um diretório de origem de dados, especifique o diretório onde estão localizados os arquivos usados com mais frequência. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório, se eles são usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONE \* DE C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando o **SQLSetConnectOption** função com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar linhas excluídas|Especifica se linhas que foram marcadas como excluídos podem ser recuperadas ou posicionadas em. Se for desmarcada, as linhas excluídas não são exibidas; Se selecionada, as linhas excluídas são tratadas o mesmo que as linhas excluídas não. O padrão é desmarcado.|Para definir essa opção dinamicamente, use o **excluído** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
