---
title: Registro atual e o tamanho do conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925691"
---
# <a name="current-record-and-size-of-recordset"></a>Registro atual e o tamanho do conjunto de registros
Esta seção descreve como localizar a posição atual do cursor na amostra **conjunto de registros** na [exemplo de código JScript para retornar um conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Registro atual  
 O registro atual no conjunto de dados corresponde ao que é apontado pela posição do cursor do **Recordset** objeto. Quando um **conjunto de registros** objeto é retornado da fonte de dados como o resultado da chamada **Recordset.Open**, **Command.Execute**, ou **Connection.Execute**  (incluindo **Connection.NamedCommand** e **Connection.StoredProcedure**), o cursor for definido para apontar para o primeiro registro. O conjunto de dados de exemplo, o registro atual inicial é as "tio Bob secas orgânico Peras" item.  
  
## <a name="size-of-recordset"></a>Tamanho do conjunto de registros  
 Para descobrir o tamanho de um **conjunto de registros** de objeto, obter o valor da **RecordCount** propriedade. Esse valor é um inteiro longo que indica o número de registros a **conjunto de registros**. Se o conjunto de dados é retornado do provedor OLEDB para Microsoft SQL Server, esse valor fornece o número de linhas retornadas. Lendo a **RecordCount** propriedade em um fechado **Recordset** causa um erro.  
  
 Se o número de registros não puder ser determinado, o valor da propriedade é -1.  
  
 O valor de **RecordCount** propriedade depende também os recursos do provedor e o tipo de cursor usado. Um cursor somente encaminhamento, o valor é -1. Para um cursor de conjunto de chaves ou estático, o valor é o número real de registros retornado a **Recordset** objeto. Um cursor dinâmico, o valor é -1 ou o número real de registros, dependendo da fonte de dados.  
  
 Um cursor que dá suporte a **Recordcount** deve trabalho mais difícil e, portanto, requer mais potência de computação, que não oferece suporte a um cursor **Recordcount**. Se você não precisa saber o número de registros, usar o tipo de cursor diferente pode ajudar a melhorar o desempenho do seu aplicativo, especialmente se você precisa lidar com um grande conjunto de dados.  
  
 Em alguns casos, um provedor ou o cursor é não é possível determinar a **RecordCount** valor sem primeiro buscar todos os registros da fonte de dados. Para garantir a contagem precisos, chame o **conjunto de registros**. **MoveLast** método antes de chamar **RecordCount**.  
  
 O exemplo **conjunto de registros** objeto obtido usando o [exemplo de código JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) usa um cursor somente encaminhamento, por isso a chamada **RecordCount** neste objeto sempre resulta em -1. Se você alterar a linha de código que chama o **conjunto de registros**. **Abra** método, conforme mostrado no exemplo a seguir, o **RecordCount** propriedade retornará o número real de registros encontrados.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Isso ocorre porque estático cursores com o [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) suporte **RecordCount**. Neste exemplo, há cinco registros e, portanto, **RecordCount** deve produzir o valor de 5.  
  
 Esta seção contém o tópico a seguir.  
  
 [Limites de um conjunto de registros](../../../ado/guide/data/boundaries-of-a-recordset.md)
