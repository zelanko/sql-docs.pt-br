---
title: SQLConfigDataSource (Driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79c4740e631df222b0fbc004bf80b80032efa19d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Driver de acesso)
> [!NOTE]  
>  Este tópico fornece informações específicas de Driver de acesso. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 O **SQLConfigDataSource** função que é usada para adicionar, modificar ou excluir uma fonte de dados dinamicamente usa as seguintes palavras-chave.  
  
|Palavra-chave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Isso define a mesma opção como **sequência de agrupamento** na caixa de diálogo de instalação.|  
|COMPACT_DB|Executa a compactação de dados em um arquivo de banco de dados. Tem o seguinte formato: COMPACT_DB = < nome_do_caminho >< optionaL_sort_order >\<palavra-chave de criptografia opcional >.<br /><br /> Ao usar a palavra-chave COMPACT_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, a compactação de um banco de dados e especificando um DSN são um processo de duas etapas.|  
|CREATE_DB|Cria um arquivo de banco de dados. Tem o seguinte formato: CREATE_DB = < nome_do_caminho >\<optional_sort ordem >< optional_ENCRYPT palavra-chave >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será como conjunto de backup na caixa de diálogo novo banco de dados exibida quando o botão Criar é pressionado na caixa de diálogo Instalação do Microsoft Access. Não se for especificada nenhuma ordem de classificação, geral é usado.<br /><br /> Ao usar a palavra-chave CREATE_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criar um banco de dados e especificar um DSN são um processo de duas etapas. Ao usar a palavra-chave CREATE_DB, se o nome do caminho do banco de dados Microsoft Access a ser criado contém um ou mais espaços, em seguida, o nome completo do caminho devem ser colocados entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\PROGRAM FILES\COMMON MyAccess.mdb de programas \"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|CREATE_SYSDB|Cria um arquivo de banco de dados do sistema. Tem o seguinte formato: CREATE_SYSDB =\<caminho-name >\<opcional ordem de classificação >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será como conjunto de backup no **novo banco de dados** caixa de diálogo exibida quando o **criar** botão é clicado no **instalação do Microsoft Access ODBC** caixa de diálogo. Não se for especificada nenhuma ordem de classificação, geral é usado.|  
|CREATE_V2DB|Cria um arquivo de banco de dados que é compatível com o Microsoft Access 2.0. Tem o seguinte formato: CREATE_V2DB =\<caminho-name >\<opcional ordem de classificação >, onde o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho Especifica um banco de dados existente. A ordem de classificação será como conjunto de backup na caixa de diálogo novo banco de dados exibida quando o botão Criar é pressionado na caixa de diálogo Instalação do Microsoft Access. Não se for especificada nenhuma ordem de classificação, geral é usado.<br /><br /> Ao usar a palavra-chave CREATE_V2DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criar um banco de dados e especificar um DSN são um processo de duas etapas.<br /><br /> Ao usar a palavra-chave CREATE_V2DB, se o nome do caminho do banco de dados Microsoft Access a ser criado contém um ou mais espaços, em seguida, o nome completo do caminho devem ser colocados entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\PROGRAM FILES\COMMON MyAccess.mdb de programas \"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção como **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o arquivo de banco de dados.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção como **descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERID|Uma ID de inteiro para o driver.  25 (Microsoft Access)|  
|FIL|Microsoft Access para o Microsoft Access de tipo de arquivo|  
|IMPLICITCOMMITSYNC|Determina se o driver do Microsoft Access executará confirmações internas ou implícitas assincronamente. Esse valor é definido inicialmente como "Sim", que significa que o driver do Microsoft Access aguardará confirmações em uma transação interna/implícita para ser concluída.<br /><br /> O valor dessa opção não deve ser alterado sem considerar cuidadosamente as consequências. Para obter mais informações sobre a opção, consulte o *guia do programador do Microsoft Jet Database Engine*.<br /><br /> Isso define a mesma opção como **ImplicitCommitSync** na caixa de diálogo de instalação.|  
|MAXBUFFERSIZE|O tamanho do buffer interno, em quilobytes, que é usado pelo Microsoft Access para transferir dados e para o disco. O tamanho do buffer padrão é 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser usado. Isso define a mesma opção como **tamanho do Buffer** na caixa de diálogo de instalação.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados da coluna com base em dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas a serem examinadas. O valor padrão é 8; Se estiver definido como 0, todas as linhas são examinadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção como **linhas a examinar** na caixa de diálogo de instalação.|  
|PAGETIMEOUT|Especifica o período de tempo, em milissegundos, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é cinco-décimos de segundo (0,5 segundo). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **Page Timeout** na caixa de diálogo de instalação.|  
|PWD|A senha.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não é somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|REPAIR_DB|Repara um banco de dados danificado por uma falha que ocorre durante o processo de confirmação.<br /><br /> Ao usar a palavra-chave REPAIR_DB na mesma instrução com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, reparar um banco de dados e especificando um DSN são um processo de duas etapas.|  
|SYSTEMDB|Para o driver do Microsoft Access, a especificação do caminho para o arquivo de banco de dados do sistema.<br /><br /> Isso define a mesma opção como **banco de dados do sistema** na caixa de diálogo de instalação.|  
|THREADS|O número de threads de plano de fundo para o mecanismo de usar. Esse valor padrão é 3, mas pode ser alterado.<br /><br /> Isso define a mesma opção como **Threads** na caixa de diálogo de instalação.|  
|UID|Para o driver do Microsoft Access, o nome da ID de usuário usado para logon.|  
|USERCOMMITSYNC|Determina se o driver do Microsoft Access será executado assincronamente transações definidas pelo usuário. Esse valor é definido inicialmente como "Sim", que significa que o driver do Microsoft Access aguardará confirmações em uma transação definida pelo usuário para ser concluída.<br /><br /> O valor dessa opção não deve ser alterado sem considerar cuidadosamente as consequências. Para obter mais informações sobre a opção, consulte o *guia do programador do Microsoft Jet Database Engine*.<br /><br /> Isso define a mesma opção como **UserCommitSync** na caixa de diálogo de instalação.|
