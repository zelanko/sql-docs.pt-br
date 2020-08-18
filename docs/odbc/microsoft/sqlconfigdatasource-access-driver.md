---
description: SQLConfigDataSource (Driver do Access)
title: SQLConfigDataSource (driver de acesso) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411982"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de acesso. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource** que é usada para adicionar, modificar ou excluir uma fonte de dados usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Isso define a mesma opção que a **sequência de agrupamento** na caixa de diálogo de instalação.|  
|COMPACT_DB|Executa a compactação de dados em um arquivo de banco de dado. Tem o seguinte formato: COMPACT_DB =<path_name><optionaL_sort_order>\<optional ENCRYPT keyword> .<br /><br /> Ao usar a palavra-chave COMPACT_DB na mesma instrução com uma palavra-chave DSN, esse driver ignora a palavra-chave DSN. Portanto, a compactação de um banco de dados e a especificação de um DSN é um processo de duas etapas.|  
|CREATE_DB|Cria um arquivo de banco de dados. Tem o seguinte formato: CREATE_DB =<path_name><\<optional_sort-order> palavra-chave optional_ENCRYPT, em que o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será definida na caixa de diálogo novo banco de dados exibida quando o botão criar for pressionado na caixa de diálogo configuração do Microsoft Access. Se nenhuma ordem de classificação for especificada, o geral será usado.<br /><br /> Ao usar a palavra-chave CREATE_DB na mesma instrução com uma palavra-chave DSN, esse driver ignora a palavra-chave DSN. Portanto, a criação de um banco de dados e a especificação de um DSN é um processo de duas etapas. Ao usar a palavra-chave CREATE_DB, se o nome do caminho do banco de dados do Microsoft Access a ser criado contiver um ou mais espaços, o nome do caminho inteiro deverá estar entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\Arquivos de PROGRAMAS\ARQUIVOS arquivos \ myaccess. mdb"<br /><br /> "C:\Arquivos de FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (sem aspas necessárias)|  
|CREATE_SYSDB|Cria um arquivo de banco de dados do sistema. Tem o seguinte formato: CREATE_SYSDB = \<path-name> \<optional-sort-order> , em que o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será definida na caixa de diálogo **novo banco de dados** exibida quando o botão **criar** for clicado na caixa de diálogo **configuração do ODBC do Microsoft Access** . Se nenhuma ordem de classificação for especificada, o geral será usado.|  
|CREATE_V2DB|Cria um arquivo de banco de dados compatível com o Microsoft Access 2,0. Tem o seguinte formato: CREATE_V2DB = \<path-name> \<optional-sort-order> , em que o nome do caminho é o caminho completo para um banco de dados do Microsoft Access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será definida na caixa de diálogo novo banco de dados exibida quando o botão criar for pressionado na caixa de diálogo configuração do Microsoft Access. Se nenhuma ordem de classificação for especificada, o geral será usado.<br /><br /> Ao usar a palavra-chave CREATE_V2DB na mesma instrução com uma palavra-chave DSN, esse driver ignora a palavra-chave DSN. Portanto, a criação de um banco de dados e a especificação de um DSN é um processo de duas etapas.<br /><br /> Ao usar a palavra-chave CREATE_V2DB, se o nome do caminho do banco de dados do Microsoft Access a ser criado contiver um ou mais espaços, o nome do caminho inteiro deverá estar entre aspas duplas, conforme mostrado nos exemplos a seguir:<br /><br /> "C:\Arquivos de PROGRAMAS\ARQUIVOS arquivos \ myaccess. mdb"<br /><br /> "C:\Arquivos de FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (sem aspas necessárias)|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção que o **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o arquivo de banco de dados.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção que a **Descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERid|Uma ID de inteiro para o driver.  25 (Microsoft Access)|  
|FIL|Tipo de arquivo MS Access para Microsoft Access|  
|IMPLICITCOMMITSYNC|Determina se o driver do Microsoft Access executará confirmações internas ou implícitas de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará a conclusão de confirmações em uma transação interna/implícita.<br /><br /> O valor dessa opção não deve ser alterado sem uma consideração cuidadosa das consequências. Para obter mais informações sobre a opção, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.<br /><br /> Isso define a mesma opção que **ImplicitCommitSync** na caixa de diálogo de instalação.|  
|MAXBUFFERSIZE|O tamanho do buffer interno, em kilobytes, que é usado pelo Microsoft Access para transferir dados de e para o disco. O tamanho de buffer padrão é 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser usado. Isso define a mesma opção de **tamanho do buffer** na caixa de diálogo de instalação.|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas a serem verificadas. O valor padrão é 8; Se for definido como 0, todas as linhas serão verificadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção que as **linhas a serem verificadas** na caixa de diálogo de instalação.|  
|PAGETIMEOUT|Especifica o período de tempo, em milissegundos, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é cinco décimos de segundo (0,5 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **tempo limite de página** na caixa de diálogo de instalação.|  
|PWD|A senha.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|REPAIR_DB|Repara um banco de dados danificado por uma falha que ocorre durante o processo de confirmação.<br /><br /> Ao usar a palavra-chave REPAIR_DB na mesma instrução com uma palavra-chave DSN, esse driver ignora a palavra-chave DSN. Portanto, reparar um banco de dados e especificar um DSN é um processo de duas etapas.|  
|SYSTEMDB|Para o driver do Microsoft Access, a especificação de caminho para o arquivo de banco de dados do sistema.<br /><br /> Isso define a mesma opção que o **banco de dados do sistema** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano a ser usado pelo mecanismo. O padrão desse valor é 3, mas pode ser alterado.<br /><br /> Isso define a mesma opção que os **threads** na caixa de diálogo de instalação.|  
|UID|Para o driver do Microsoft Access, o nome da ID de usuário usado para logon.|  
|USERCOMMITSYNC|Determina se o driver do Microsoft Access irá executar transações definidas pelo usuário de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará a conclusão de confirmações em uma transação definida pelo usuário.<br /><br /> O valor dessa opção não deve ser alterado sem uma consideração cuidadosa das consequências. Para obter mais informações sobre a opção, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.<br /><br /> Isso define a mesma opção que **UserCommitSync** na caixa de diálogo de instalação.|
