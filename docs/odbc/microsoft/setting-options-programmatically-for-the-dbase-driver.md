---
title: Definindo opções programaticamente para o driver do dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300776"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Configurar opções programaticamente para drivers do dBASE

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Contagem aproximada de linhas|Determina se as estatísticas de tamanho de tabela são aproximadas. Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.|Para definir essa opção dinamicamente, use a palavra-chave **Statistics** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sequência de agrupamento|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou internacional.|Para definir essa opção dinamicamente, use a palavra-chave **COLLATINGSEQUENCE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou equipe.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dado. Se nenhum banco de dados for fornecido na instalação, os usuários receberão uma solicitação para selecionar um arquivo de banco de dados quando eles se conectarem à fonte.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "data de contratação, histórico de salários e revisão atual de todos os funcionários".|Para definir essa opção dinamicamente, use a palavra-chave **Description** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Se a caixa **exclusiva** for selecionada, o banco de dados será aberto em modo exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado quando executado em modo exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **Exclusive** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tempo limite da página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **ReadOnly** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Ao definir um diretório de fonte de dados, especifique o diretório onde os arquivos usados com mais frequência estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONAR \* de C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar linhas excluídas|Especifica se as linhas que foram marcadas como excluídas podem ser recuperadas ou posicionadas em. Se estiverem desmarcadas, as linhas excluídas não serão exibidas; Se selecionado, as linhas excluídas serão tratadas da mesma forma que as linhas não excluídas. O padrão é limpo.|Para definir essa opção dinamicamente, use a palavra-chave **Deleted** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
