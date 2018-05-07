---
title: Registro atual e o tamanho do conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47039bdba7fe5d5a867df4ac7ca8700a7a835b13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="current-record-and-size-of-recordset"></a>Registro atual e o tamanho do conjunto de registros
Esta seção descreve como localizar a posição atual do cursor no exemplo **registros** na [JScript exemplo de código para retornar um conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Registro atual  
 O registro atual no conjunto de dados corresponde ao que aponta para a posição do cursor do **registros** objeto. Quando um **registros** objeto é retornado da fonte de dados como o resultado da chamada **Recordset.Open**, **Command.Execute**, ou **Connection.Execute**  (incluindo **Connection.NamedCommand** e **Connection.StoredProcedure**), o cursor é definido para apontar para o primeiro registro. O conjunto de dados de exemplo, o registro atual inicial é as "do Tio Paulo secas orgânicos Peras" item.  
  
## <a name="size-of-recordset"></a>Tamanho do conjunto de registros  
 Para descobrir o tamanho de um **registros** de objeto, obter o valor da **RecordCount** propriedade. Esse valor é um inteiro longo que indica o número de registros a **registros**. Se o conjunto de dados é retornado do provedor OLEDB para Microsoft SQL Server, esse valor retorna o número de linhas retornadas. Lendo o **RecordCount** propriedade em um fechado **registros** causa um erro.  
  
 Se o número de registros não puder ser determinado, o valor da propriedade é -1.  
  
 O valor de **RecordCount** propriedade também depende dos recursos do provedor e o tipo de cursor usado. Para um cursor de somente avanço, o valor será -1. Para um cursor estático ou o conjunto de chaves, o valor é o número real de registros retornados no **registros** objeto. Para um cursor dinâmico, o valor é -1 ou o número real de registros, dependendo da fonte de dados.  
  
 Um cursor que dá suporte a **Recordcount** deve trabalho mais difícil e, portanto, requer mais potência de computação, que não oferece suporte a um cursor **Recordcount**. Se você não precisa saber o número de registros, usar o tipo de cursor diferente pode ajudar a melhorar o desempenho do aplicativo, especialmente se você precisa lidar com um grande conjunto de dados.  
  
 Em alguns casos, um provedor ou o cursor é não é possível determinar o **RecordCount** valor sem primeiro buscar todos os registros da fonte de dados. Para garantir a contagem precisas, chame o **registros**. **MoveLast** método antes de chamar **RecordCount**.  
  
 O exemplo **registros** objeto obtido usando o [exemplo de código JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) usa um cursor somente encaminhamento, por isso a chamada **RecordCount** neste objeto sempre resulta em – 1. Se você alterar a linha de código que chama o **registros**. **Abra** método conforme mostrado no exemplo a seguir, o **RecordCount** propriedade retornará o número real de registros encontrados.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Isso ocorre porque estático cursores com o [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) suporte **RecordCount**. Neste exemplo, há cinco registros e, portanto, **RecordCount** deve produzir um valor de 5.  
  
 Esta seção contém o tópico a seguir.  
  
 [Limites de um conjunto de registros](../../../ado/guide/data/boundaries-of-a-recordset.md)
