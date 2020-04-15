---
title: Definindo opções Programáticamente para o driver dBASE | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300776"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Configurar opções programaticamente para drivers do dBASE

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Contagem aproximada da linha|Determina se as estatísticas de tamanho da tabela são aproximadas. Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.|Para definir essa opção dinamicamente, use a palavra-chave **STATISTICS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seqüência de colisão|A seqüência em que os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou Internacional.|Para definir essa opção dinamicamente, use a palavra-chave **COLLATINGSEQUENCE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como Folha de Pagamento ou Pessoal.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados for fornecido após a configuração, os usuários serão solicitados a selecionar um arquivo de banco de dados quando eles se conectarem à fonte de dados.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "Data de contratação, histórico salarial e revisão atual de todos os funcionários."|Para definir essa opção dinamicamente, use a palavra-chave **DESCRIPTION** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Se a caixa **Exclusiva** for selecionada, o banco de dados será aberto no modo Exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado quando é executado no modo Exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **EXCLUSIVE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tempo de página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo de saída da página não pode ser 0 por causa de um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **READONLY** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contenha os arquivos que deseja acessar.<br /><br /> Quando você definir um diretório de origem de dados, especifique o diretório onde seus arquivos mais usados estão localizados. O driver ODBC usa este diretório como o diretório padrão. Copie outros arquivos neste diretório se eles forem usados com freqüência. Alternativamente, você pode qualificar nomes de arquivos em uma declaração SELECT com o nome do diretório:<br /><br /> SELECIONE \* C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar linhas excluídas|Especifica se as linhas que foram marcadas como excluídas podem ser recuperadas ou posicionadas. Se limpas, as linhas excluídas não serão exibidas; se selecionadas, as linhas excluídas são tratadas da mesma forma que linhas não excluídas. O padrão é limpo.|Para definir essa opção dinamicamente, use a palavra-chave **EXCLUÍDA** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
