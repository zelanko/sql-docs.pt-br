---
title: Definindo opções programáticas para o Driver Paradoxo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300756"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Configurar opções programaticamente para drivers do Paradox

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Diretório|Define o diretório direcionado.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seqüência de colisão|A seqüência em que os campos são classificados.<br /><br /> A sequência pode ser ASCII (o padrão), internacional, sueco-finlandês ou norueguês-dinamarquês.|Para definir essa opção dinamicamente, use a palavra-chave **COLLATINGSEQUENCE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "Data de contratação, histórico salarial e revisão atual de todos os funcionários."|Para definir essa opção dinamicamente, use a palavra-chave **DESCRIPTION** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Se a caixa **Exclusiva** for selecionada, o banco de dados será aberto no modo Exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado ao ser executado no modo Exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **EXCLUSIVE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo net|O estilo de acesso à rede a ser usado ao acessar dados do Paradox: ou "3.*x"* para Paradox3. *x* ou "4. *x*" para Paradox4. *x* ou 5. *x*. Pode ser definido como "3. *x*" ou "4. *x*" se a versão for Paradox 4. *x* ou 5. *x*; se a versão é Paradoxo 3. *x*, o estilo deve ser "3. *x*".|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXNETSTYLE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tempo de página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo de saída da página não pode ser 0 por causa de um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **READONLY** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório contendo os arquivos que deseja acessar.<br /><br /> Ao definir um diretório de origem de dados, especifique o diretório onde os arquivos mais usados estão localizados. O driver ODBC usa este diretório como o diretório padrão. Copie outros arquivos neste diretório se eles forem usados com freqüência. Alternativamente, você pode qualificar nomes de arquivos em uma declaração SELECT com o nome do diretório:<br /><br /> SELECIONE \* C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando a função **SQLSetConnectOption** com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use a palavra-chave **DEFAULTDIR** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecione diretório de rede|O caminho completo do diretório contendo um banco de dados de bloqueio paradoxo, porque contém o arquivo Pdoxusrs.net (no Paradox4.* x*) ou o arquivo Paradox.net (no Paradoxo 5.* x*). Se o diretório não contiver um desses arquivos, o driver Paradoxo criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradoxo.<br /><br /> Antes de selecionar um diretório de rede, você deve inserir seu nome de usuário Paradoxna na caixa de texto Nome do **Usuário.** Clique **em Selecionar diretório de rede** para selecionar um diretório de rede.|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXNETPATH** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome do Usuário|O nome de usuário do Paradoxo. Este é o nome exibido para outros usuários de arquivos Paradox quando um bloqueio é encontrado.|Para definir essa opção dinamicamente, use a palavra-chave **PARADOXUSERNAME** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
