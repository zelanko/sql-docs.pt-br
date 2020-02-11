---
title: Definindo opções programaticamente para o driver do Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063510"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Configurar opções programaticamente para drivers do Paradox

|Opção|DESCRIÇÃO|Método|  
|------------|-----------------|------------|  
|Directory|Define o diretório de destino.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequência de agrupamento|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser ASCII (o padrão), internacional, sueco-finlandês ou norueguês-dinamarquês.|Para definir essa opção dinamicamente, use a palavra-chave **COLLATINGSEQUENCE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|DESCRIÇÃO|Uma descrição opcional dos dados na fonte de dados; por exemplo, "data de contratação, histórico de salários e revisão atual de todos os funcionários".|Para definir essa opção dinamicamente, use a palavra-chave **Description** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Se a caixa **exclusiva** for selecionada, o banco de dados será aberto em modo exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado quando executado em modo exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **Exclusive** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo líquido|O estilo de acesso à rede a ser usado ao acessar dados do Paradox: "3.*x*" para o Paradox 3. *x* ou "4. *x*"para o Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. *x*"ou" 4. *x*"se a versão for o Paradox 4. *x* ou 5. *x*; se a versão for o Paradox 3. *x*, o estilo deve ser "3. *x*".|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXNETSTYLE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tempo limite da página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **ReadOnly** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde é possível selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Ao definir um diretório de fonte de dados, especifique o diretório onde os arquivos usados com mais frequência estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONAR \* de C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DefaultDir** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecionar diretório de rede|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, pois ele contém o arquivo Pdoxusrs.net (no Paradox 4.* x*) ou o arquivo Paradox.net (no Paradox 5.* x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes de selecionar um diretório de rede, você deve inserir seu nome de usuário do Paradox na caixa de texto **nome de usuário** . Clique em **Selecionar diretório de rede** para selecionar um diretório de rede.|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXNETPATH** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome de usuário|O nome de usuário do Paradox. Esse é o nome exibido para outros usuários de arquivos do Paradox quando um bloqueio é encontrado.|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXUSERNAME** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
