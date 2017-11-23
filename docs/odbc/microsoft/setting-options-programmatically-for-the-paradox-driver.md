---
title: "Opções de configuração por meio de programação para o Driver do Paradox | Microsoft Docs"
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
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c4b822a41f18250e92ed9fe4475507fef01127b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Opções de configuração por meio de programação para o Driver do Paradox
|Opção|Description|Método|  
|------------|-----------------|------------|  
|Diretório|Define o diretório de destino.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequência de agrupamento|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser ASCII (o padrão), internacional, finlandês-sueco ou dinamarquês-norueguês.|Para definir essa opção dinamicamente, use o **COLLATINGSEQUENCE** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Description|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusive|Se o **exclusivo** caixa é selecionada, o banco de dados será aberto no modo exclusivo e pode ser acessado somente por um usuário por vez. O desempenho é melhorado ao executar em modo exclusivo.|Para definir essa opção dinamicamente, use o **exclusivo** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo da rede|O estilo de acesso de rede a ser usado ao acessar dados Paradox: o "3.*x*" para o Paradox 3. *x* ou "4. *x*"para o Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. *x*"ou" 4. *x*"se a versão for Paradox 4. *x* ou 5. *x*; se a versão for Paradox 3. *x*, o estilo deve ser "3. *x*".|Para definir essa opção dinamicamente, use o **PARADOXNETSTYLE** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tempo limite da página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo se a opção de tempo limite de página está definida abaixo do valor.|Para definir essa opção dinamicamente, use o **PAGETIMEOUT** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecione o diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Quando a definição de um diretório de origem de dados especifica o diretório onde o mais comumente usados arquivos estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório, se eles são usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONE \* DE C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando o **SQLSetConnectOption** função com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecione o diretório de rede|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, porque ele contém o arquivo Pdoxusrs.net (no Paradox 4. *x*) ou o arquivo Paradox.net (no Paradox 5. *x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes de selecionar um diretório de rede, você deve inserir seu nome de usuário no Paradox o **nome de usuário** caixa de texto. Clique em **Selecionar pasta de rede** para selecionar um diretório de rede.|Para definir essa opção dinamicamente, use o **PARADOXNETPATH** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome do Usuário|O nome de usuário do Paradox. Esse é o nome exibido para outros usuários de arquivos do Paradox quando um bloqueio é encontrado.|Para definir essa opção dinamicamente, use o **PARADOXUSERNAME** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
