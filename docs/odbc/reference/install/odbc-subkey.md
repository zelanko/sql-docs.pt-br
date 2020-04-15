---
title: Subkey ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287436"
---
# <a name="odbc-subkey"></a>Subchave do ODBC
Os valores sob a sub-tecla ODBC especificam opções de rastreamento ODBC. Essas opções são definidas através da guia Rastreamento da caixa de diálogo Administrador de Origem de Dados ODBC exibida pelo **SQLManageDataSources**. O subchave ODBC em si é opcional. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 Os valores têm os significados descritos na tabela a seguir.  
  
|Valor|Significado|  
|-----------|-------------|  
|Trace|Se o valor do Trace for definido como 1 quando um aplicativo chamar **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento será ativado para o aplicativo de chamada.<br /><br /> Se a palavra-chave Trace estiver definida como 0 quando um aplicativo chamar **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento será desativado para o aplicativo de chamada. Esse é o valor padrão.<br /><br /> Um aplicativo pode ativar ou desativar o rastreamento com o atributo de conexão SQL_ATTR_TRACE. No entanto, fazer isso não altera os dados para este valor.|  
|TraceFile|Se o rastreamento estiver ativado, o Gerenciador de drivers será substituído no arquivo de rastreamento especificado pelo valor TraceFile.<br /><br /> Se nenhum arquivo de rastreamento for especificado, o Driver Manager será substituído no arquivo Sql.log na unidade atual. Esse é o valor padrão.<br /><br /> O rastreamento deve ser usado apenas para um único aplicativo, ou cada aplicativo deve especificar um arquivo de rastreamento diferente. Caso contrário, dois ou mais aplicativos tentarão abrir o mesmo arquivo de rastreamento ao mesmo tempo, causando um erro.<br /><br /> Um aplicativo pode especificar um novo arquivo de rastreamento com o atributo de conexão SQL_ATTR_TRACEFILE. No entanto, fazer isso não altera os dados para este valor.|  
  
 Por exemplo, suponha que o rastreamento esteja ativado e que o arquivo de rastreamento seja C:\Odbc.log. Os valores sob a sub-tecla ODBC seriam os seguintes:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
