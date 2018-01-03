---
title: "Opções de configuração por meio de programação para o Driver de acesso | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81ec270afc5c0e845bea829a1851b00bb38fa075
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Opções de configuração por meio de programação para o Driver de acesso
|Opção|Description|Método|  
|------------|-----------------|------------|  
|Tamanho do buffer|O tamanho do buffer interno, em quilobytes, que é usado pelo Microsoft Access para transferir dados e para o disco. O tamanho do buffer padrão é 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser inserido.|Para definir essa opção dinamicamente, use a palavra-chave MAXBUFFERSIZE em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou pessoal.|Para definir essa opção dinamicamente, use o **DSN** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados é fornecido após a instalação, o usuário será solicitado a escolher um arquivo de banco de dados ao conectar-se à fonte de dados.|Para definir essa opção dinamicamente, use o **DBQ** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Description|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusive|Se o **exclusivo** caixa é selecionada, o banco de dados será aberto no modo exclusivo e pode ser acessado somente por um usuário por vez. O desempenho é melhorado ao executar em modo exclusivo.|Para definir essa opção dinamicamente, use o **exclusivo** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina como as alterações feitas fora de uma transação são gravadas no banco de dados. Esse valor é definido inicialmente como "Sim", que significa que o driver do Microsoft Access aguardará confirmações em uma transação interna/implícita para ser concluída.|Essa opção é incluída no **definir opções avançadas** caixa de diálogo para o driver do Microsoft Access.|  
|Tempo limite da página|Especifica o período de tempo, em milissegundos, que uma página (se não usado) permanece no buffer antes de serem removidos. Para o driver do Microsoft Access, o padrão é 500 milissegundos (0,5 segundo). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo se a opção de tempo limite de página está definida abaixo do valor.|Para definir essa opção dinamicamente, use o **PAGETIMEOUT** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Banco de dados do sistema|O caminho completo do banco de dados Microsoft Access sistema a ser usado com o banco de dados do Microsoft Access que você deseja acessar.<br /><br /> Clique o **banco de dados do sistema** para selecionar o banco de dados do sistema a ser usado. O driver ODBC Microsoft Access solicita ao usuário um nome e uma senha. O nome padrão é Admin e a senha padrão do Microsoft Access para o usuário administrador é uma cadeia de caracteres vazia.<br /><br /> Para aumentar a segurança de seu banco de dados do Microsoft Access, crie um novo usuário para substituir o usuário administrador e excluir o usuário administrador ou alterar os objetos aos quais o usuário administrador tem acesso.|Para definir essa opção dinamicamente, use o **SYSTEMDB** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|O número de threads de plano de fundo para o mecanismo de usar. Para o driver do Microsoft Access, esse valor padrão é 3, mas pode ser alterado. O usuário pode desejar aumentar o número de threads se houver uma grande quantidade de atividade no banco de dados.<br /><br /> Essa opção é incluída no **definir opções avançadas** caixa de diálogo para o driver do Microsoft Access.|Para definir essa opção dinamicamente, use o **THREADS** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina se o driver do Microsoft Access executará um transações explícitas definidas pelo usuário assincronamente. Esse valor é definido inicialmente como "Sim", que significa que o driver do Microsoft Access aguardará confirmações em uma transação definida pelo usuário para ser concluída.<br /><br /> Definir essa opção como False pode ter consequências imprevisíveis em um ambiente multiusuário.|Para definir essa opção dinamicamente, use o **USERCOMMITSYNC** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
