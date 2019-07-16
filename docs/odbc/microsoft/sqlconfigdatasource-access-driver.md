---
title: SQLConfigDataSource (Driver do Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b515ed4c30d68e62a49e1044c4ddf6f5cc5ab1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985239"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver do Access. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados usa as seguintes palavras-chave dinamicamente.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|COMPACT_DB|Executa a compactação de dados em um arquivo de banco de dados. Tem o seguinte formato: COMPACT_DB = < path_name >< optionaL_sort_order >\<palavra-chave de criptografia opcional >.<br /><br /> Ao usar a palavra-chave COMPACT_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, a compactação de um banco de dados e especificando um DSN são um processo em duas etapas.|  
|CREATE_DB|Cria um arquivo de banco de dados. Tem o seguinte formato: CREATE_DB = < path_name >\<optional_sort ordem >< optional_ENCRYPT palavra-chave >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será ser conforme definido na caixa de diálogo novo banco de dados exibida quando o botão Criar é pressionado na caixa de diálogo de instalação do Microsoft Access. Se nenhuma ordem de classificação for especificada, geral é usado.<br /><br /> Ao usar a palavra-chave CREATE_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criando um banco de dados e especificando um DSN são um processo em duas etapas. Ao usar a palavra-chave CREATE_DB, se o nome do caminho do banco de dados Microsoft Access a ser criado contém um ou mais espaços, em seguida, o nome do caminho inteiro deve estar entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|CREATE_SYSDB|Cria um arquivo de banco de dados do sistema. Tem o seguinte formato: CREATE_SYSDB =\<caminho-name >\<opcional ordem de classificação >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será ser conforme definido na **novo banco de dados** caixa de diálogo exibida quando o **Create** botão é clicado no **configuração de acesso do Microsoft ODBC** caixa de diálogo. Se nenhuma ordem de classificação for especificada, geral é usado.|  
|CREATE_V2DB|Cria um arquivo de banco de dados que é compatível com o Microsoft Access 2.0. Tem o seguinte formato: CREATE_V2DB =\<caminho-name >\<opcional ordem de classificação >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será ser conforme definido na caixa de diálogo novo banco de dados exibida quando o botão Criar é pressionado na caixa de diálogo de instalação do Microsoft Access. Se nenhuma ordem de classificação for especificada, geral é usado.<br /><br /> Ao usar a palavra-chave CREATE_V2DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criando um banco de dados e especificando um DSN são um processo em duas etapas.<br /><br /> Ao usar a palavra-chave CREATE_V2DB, se o nome do caminho do banco de dados Microsoft Access a ser criado contém um ou mais espaços, em seguida, o nome do caminho inteiro deve estar entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção como **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o arquivo de banco de dados.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.  25 (Microsoft Access)|  
|FIL|Tipo MS Access para o Microsoft Access de arquivo|  
|IMPLICITCOMMITSYNC|Determina se o driver do Microsoft Access será executado assincronamente confirmações internas ou implícitas. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará confirmações em uma transação interna/implícita para ser concluída.<br /><br /> O valor dessa opção não deve ser alterado sem uma consideração cuidadosa as consequências. Para obter mais informações sobre a opção, consulte a *guia do programador do Microsoft Jet banco de dados Engine*.<br /><br /> Isso define a mesma opção como **ImplicitCommitSync** na caixa de diálogo de instalação.|  
|MAXBUFFERSIZE|O tamanho do buffer interno, em quilobytes, que é usado pelo Microsoft Access para transferir dados para e do disco. O tamanho do buffer padrão é 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser usado. Isso define a mesma opção como **tamanho do Buffer** na caixa de diálogo de instalação.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados da coluna com base nos dados existentes.<br /><br /> Um número entre 1 e 16 pode ser inserido para as linhas a serem examinadas. O valor padrão é 8; Se ele for definido como 0, todas as linhas são verificadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção como **linhas a examinar** na caixa de diálogo de instalação.|  
|PAGETIMEOUT|Especifica o período de tempo, em milissegundos, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é cinco-décimos de segundo (0,5 segundo). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|PWD|A senha.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|REPAIR_DB|Repara um banco de dados danificado por uma falha que ocorre durante o processo de confirmação.<br /><br /> Ao usar a palavra-chave REPAIR_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, a reparação de um banco de dados e especificando um DSN são um processo em duas etapas.|  
|SYSTEMDB|Para o driver do Microsoft Access, a especificação de caminho para o arquivo de banco de dados do sistema.<br /><br /> Isso define a mesma opção como **banco de dados do sistema** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano para o mecanismo a ser usado. Esse valor padrão é 3, mas pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|  
|UID|Para o driver do Microsoft Access, o nome da ID de usuário usadas para logon.|  
|USERCOMMITSYNC|Determina se o driver do Microsoft Access irá executar transações definidas pelo usuário de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará confirmações em uma transação definida pelo usuário para ser concluída.<br /><br /> O valor dessa opção não deve ser alterado sem uma consideração cuidadosa as consequências. Para obter mais informações sobre a opção, consulte a *guia do programador do Microsoft Jet banco de dados Engine*.<br /><br /> Isso define a mesma opção como **UserCommitSync** na caixa de diálogo de instalação.|
