---
title: Resumo da função do instalador DLL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddaf20334a84833433961a49e17724d354945c5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298766"
---
# <a name="installer-dll-function-summary"></a>Resumo de funções de DLL do instalador
A tabela a seguir descreve as funções no instalador DLL. Para obter mais informações sobre a sintaxe e semântica de cada função, consulte [Installer DLL API Reference](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Tarefa|Nome da função|Finalidade|  
|----------|-------------------|-------------|  
|Instalação da ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carrega a Configuração DLL específica do driver.|  
||[SQLGetDrivers instalados](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Retorna uma lista de drivers instalados.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Adiciona um driver às informações do sistema.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Retorna o diretório de destino para o Driver Manager.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Retorna informações de erro ou status para as funções do instalador.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Adiciona um tradutor às informações do sistema.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Permite que uma biblioteca de configuração de driver ou tradutor reporte erros.|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Remove as informações de um driver do sistema.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Remove os componentes principais do ODBC das informações do sistema.|  
||[SQLRemoveTradutor](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Remove as informações do tradutor do sistema.|  
|Configurando fontes de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Chama a configuração específica do driver De llLl.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Exibe uma caixa de diálogo para adicionar uma fonte de dados.|  
||[Modo SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera o modo de configuração que indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema.|  
||[SqlGetPrivateProfilestring](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Escreve um valor para as informações do sistema.|  
||[SqlGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Exibe uma caixa de diálogo para selecionar um tradutor.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Exibe uma caixa de diálogo para configurar fontes de dados e drivers.|  
||[SQlReadfiledsn](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Lê informações de DSNs de arquivo.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Remove a fonte de dados padrão.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Remove uma fonte de dados.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Define o modo de configuração que indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema.|  
||[SQLvaliddSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Verifica o comprimento e a validade do nome da fonte de dados.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Adiciona uma fonte de dados.|  
||[SQLWritefileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Grava informações para arquivar DSNs.|  
||[SQLWritePrivateProfilestring](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Obtém um valor das informações do sistema.|
