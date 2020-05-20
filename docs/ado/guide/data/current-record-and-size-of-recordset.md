---
title: Registro e tamanho atuais do conjunto de registros | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 30b669a566270a0eff5d6cf93abb5b0acb7ff3c2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761122"
---
# <a name="current-record-and-size-of-recordset"></a>Registro atual e o tamanho do conjunto de registros
Esta seção descreve como localizar a posição atual do cursor no **conjunto de registros** de exemplo no [exemplo de código JScript para retornar um conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Registro atual  
 O registro atual no conjunto de registros corresponde àquele apontado pela posição do cursor do objeto **Recordset** . Quando um objeto **Recordset** é retornado da fonte de dados como resultado da chamada de **Recordset. Open**, **Command. Execute**ou **Connection. Execute** (incluindo **Connection. NamedCommand** e **Connection. StoredProcedure**), o cursor é definido para apontar para o primeiro registro. No conjunto de exemplos, o registro atual inicial é o item "pêras secas orgânicas do tio Bob".  
  
## <a name="size-of-recordset"></a>Tamanho do conjunto de registros  
 Para descobrir o tamanho de um objeto **Recordset** , obtenha o valor da propriedade **Recordset. RecordCount** . Esse valor é um inteiro longo que indica o número de registros no **conjunto**de registros. Se o conjunto de registros for retornado do provedor OLEDB para Microsoft SQL Server, esse valor fornecerá o número de linhas retornadas. A leitura da propriedade **RecordCount** em um **conjunto de registros** fechado causa um erro.  
  
 Se o número de registros não puder ser determinado, o valor da propriedade será-1.  
  
 O valor da propriedade **RecordCount** também depende dos recursos do provedor e do tipo de cursor usado. Para um cursor de somente avanço, o valor é-1. Para um cursor estático ou de conjunto de chaves, o valor é o número real de registros retornados no objeto **Recordset** . Para um cursor dinâmico, o valor é-1 ou o número real de registros, dependendo da fonte de dados.  
  
 Um cursor que dá suporte a **RecordCount** deve funcionar mais e, portanto, requer mais capacidade computacional, do que um cursor não dá suporte a **RecordCount**. Se você não precisar saber o número de registros, usar o tipo de cursor diferente pode ajudar a melhorar o desempenho do aplicativo, especialmente se você precisar lidar com um grande conjunto de dados.  
  
 Em alguns casos, um provedor ou cursor não pode determinar o valor de **RecordCount** sem primeiro buscar todos os registros da fonte de dados. Para garantir a contagem precisa, chame o **conjunto de registros**. Método **MoveLast** antes de chamar **Recordset. RecordCount**.  
  
 O objeto **Recordset** de exemplo obtido usando o [exemplo de código JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) usa um cursor de somente avanço, portanto, chamar **RecordCount** nesse objeto sempre resulta em-1. Se você alterar a linha de código que chama o **conjunto de registros**. **Abrir** o método, conforme mostrado no exemplo a seguir, a propriedade **RecordCount** retornará o número real de registros buscados.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Isso ocorre porque cursores estáticos com o [provedor de OLE DB da Microsoft para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) dão suporte a **RecordCount**. Neste exemplo, há cinco registros e, portanto, o **RecordCount** deve produzir o valor de 5.  
  
 Esta seção contém o tópico a seguir.  
  
 [Limites de um conjunto de registros](../../../ado/guide/data/boundaries-of-a-recordset.md)
