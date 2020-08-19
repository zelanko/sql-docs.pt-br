---
description: Métodos RDS
title: Métodos RDS | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f8685ead3b7f62861d6e27792a850af3140ebe3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438788"
---
# <a name="rds-methods"></a>Métodos RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Método|Descrição|  
|-|-|  
|[Cancelar (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)|Cancela a execução de uma chamada de método pendente e assíncrona.|  
|[CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)|Cancela as alterações feitas na linha atual ou nova de um objeto **Recordset** .|  
|[ConvertTostring (RDS)](../../../ado/reference/rds-api/converttostring-method-rds.md)|Converte um **conjunto de registros** em uma cadeia de caracteres MIME que representa os dados do conjunto de registros.|  
|[CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)|Cria o proxy para o objeto comercial de destino e retorna um ponteiro para ele.|  
|[Isrecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|Cria um **conjunto de registros**vazio e desconectado.|  
|[Método Execute (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)|Execute a solicitação e crie um conjunto de linhas de dados avançado (para uso com ADO 2,5 e posterior).|  
|[Método Execute21 (RDS)](../../../ado/reference/rds-api/execute21-method-rds.md)|Execute a solicitação e crie um conjunto de linhas de dados avançado (para uso com ADO 2,1).|  
|[InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md)|Retorna um ponteiro para a interface solicitada em uma versão mais compatível do objeto.|  
|[MoveFirst, MoveLast, MoveNext, MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|Move para o primeiro, o último, o próximo ou o registro anterior em um objeto **Recordset** especificado.|  
|[Consulta (RDS)](../../../ado/reference/rds-api/query-method-rds.md)|Usa uma cadeia de caracteres de consulta SQL válida para retornar um **conjunto de registros**.|  
|[Atualizar (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)|Consulta novamente a fonte de dados especificada na propriedade **Connect** e atualiza os resultados da consulta.|  
|[Redefinir (RDS)](../../../ado/reference/rds-api/reset-method-rds.md)|Executa a classificação ou o filtro em um **conjunto de registros**do lado do cliente, com base nas propriedades de classificação e filtro especificadas.|  
|[SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)|Envia alterações pendentes do **conjunto de registros** armazenado em cache e atualizável localmente para a fonte de dados especificada na propriedade **Connect** .|  
|[Método Synchronize (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)|Sincronize o conjunto de registros fornecido com o banco de dados especificado pela cadeia de conexão (para uso com o ADO 2,5 e posterior).|  
|[Método Synchronize21 (RDS)](../../../ado/reference/rds-api/synchronize21-method-rds.md)|Sincronize o conjunto de registros fornecido com o banco de dados especificado pela cadeia de conexão (para uso com ADO 2,1).|


