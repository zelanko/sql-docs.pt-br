---
title: "Resumo de função DLL do instalador | Microsoft Docs"
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
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fcd7785696a49659c5d2e19cd4d5645624c52e6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="installer-dll-function-summary"></a>Resumo de função DLL do instalador
A tabela a seguir descreve as funções no instalador do DLL. Para obter mais informações sobre a sintaxe e semântica para cada função, consulte [referência de API do instalador DLL](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Tarefa|Nome da função|Finalidade|  
|----------|-------------------|-------------|  
|Instalando ODBC|[No SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carrega a DLL de configuração específica do driver.|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Retorna uma lista de drivers instalados.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Adiciona um driver para as informações do sistema.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Retorna o diretório de destino para o Gerenciador de Driver.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Retorna informações de erro ou de status para as funções do instalador.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Adiciona um tradutor para as informações do sistema.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Permite que uma biblioteca de instalação de driver ou conversor para relatar erros.|  
||[No SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Remove um driver das informações do sistema.|  
||[No SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Remove os principais componentes ODBC das informações do sistema.|  
||[No SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Remove o tradutor das informações do sistema.|  
|Configurando fontes de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Chama o DLL de configuração específica do driver.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Exibe uma caixa de diálogo para adicionar uma fonte de dados.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera o modo de configuração que indica onde a entrada Odbc.ini listando valores DSN é nas informações do sistema.|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Grava um valor para as informações do sistema.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Exibe uma caixa de diálogo para selecionar um conversor.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Exibe uma caixa de diálogo para configurar os drivers e fontes de dados.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Lê as informações de DSNs de arquivos.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Remove a fonte de dados padrão.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Remove uma fonte de dados.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Define o modo de configuração que indica onde a entrada Odbc.ini listando valores DSN é nas informações do sistema.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Verifica o comprimento e a validade do nome de fonte de dados.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Adiciona uma fonte de dados.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Grava informações de DSNs de arquivos.|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Obtém um valor das informações do sistema.|
