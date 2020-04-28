---
title: Subchave ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287436"
---
# <a name="odbc-subkey"></a>Subchave do ODBC
Os valores na subchave ODBC especificam opções de rastreamento ODBC. Essas opções são definidas por meio da guia rastreamento da caixa de diálogo administrador de fonte de dados ODBC exibida por **SQLManageDataSources**. A própria subchave ODBC é opcional. O formato desses valores é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*TraceFile-caminho*|  
  
 Os valores têm os significados descritos na tabela a seguir.  
  
|Valor|Significado|  
|-----------|-------------|  
|Trace|Se o valor de rastreamento for definido como 1 quando um aplicativo chamar **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento será habilitado para o aplicativo de chamada.<br /><br /> Se a palavra-chave Trace for definida como 0 quando um aplicativo chamar **SQLAllocHandle** com a opção SQL_HANDLE_ENV, o rastreamento será desabilitado para o aplicativo de chamada. Este é o valor padrão.<br /><br /> Um aplicativo pode habilitar ou desabilitar o rastreamento com o atributo de conexão SQL_ATTR_TRACE. No entanto, isso não altera os dados para esse valor.|  
|TraceFile|Se o rastreamento estiver habilitado, o Gerenciador de driver gravará no arquivo de rastreamento especificado pelo valor de TraceFile.<br /><br /> Se nenhum arquivo de rastreamento for especificado, o Gerenciador de driver gravará no arquivo SQL. log na unidade atual. Este é o valor padrão.<br /><br /> O rastreamento deve ser usado somente para um único aplicativo, ou cada aplicativo deve especificar um arquivo de rastreamento diferente. Caso contrário, dois ou mais aplicativos tentarão abrir o mesmo arquivo de rastreamento ao mesmo tempo, causando um erro.<br /><br /> Um aplicativo pode especificar um novo arquivo de rastreamento com o atributo de conexão SQL_ATTR_TRACEFILE. No entanto, isso não altera os dados para esse valor.|  
  
 Por exemplo, suponha que o rastreamento esteja habilitado e o arquivo de rastreamento seja C:\Odbc.log. Os valores na subchave ODBC seriam os seguintes:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
