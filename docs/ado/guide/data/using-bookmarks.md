---
title: Usando indicadores | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fa2a738a3e94cd306619a318b75a2fd506972c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923602"
---
# <a name="using-bookmarks"></a>Usar indicadores
Geralmente, é útil retornar diretamente a um registro específico depois de movido no **conjunto de registros** sem a necessidade de percorrer cada registro e comparar valores. Por exemplo, se você tentar Pesquisar um registro usando o método **Find** , mas a pesquisa não retornar registros, você será colocado automaticamente em qualquer uma das extremidades do **conjunto de registros**. Se seu provedor oferecer suporte a eles, os indicadores poderão ser usados para marcar seu local antes de usar o método **Find** para que você possa retornar ao seu local. Um indicador é um valor de tipo **Variant** que identifica exclusivamente um registro em um objeto **Recordset** .  
  
 Você também pode usar uma matriz variante de indicadores com o método de **filtro Recordset** para filtrar em um conjunto selecionado de registros. Para obter detalhes sobre essa técnica, consulte Filtrando os resultados no tópico, [trabalhando com conjuntos de registros](../../../ado/guide/data/working-with-recordsets.md), mais adiante nesta seção.  
  
 Você pode usar a propriedade **Bookmark** para obter um indicador de um registro ou definir o registro atual em um objeto **Recordset** para o registro identificado por um indicador válido. O código a seguir usa a propriedade **Bookmark** para definir um indicador e, em seguida, retornar ao registro com indicador depois de passar para outros registros. Para determinar se o **conjunto de registros** dá suporte a indicadores, use o método **com suporte** .  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 O método de [suporte](../../../ado/reference/ado-api/supports-method.md) é abordado em mais detalhes posteriormente.  
  
 Exceto pelo caso de **conjuntos de registros**clonados, os indicadores são exclusivos do **conjunto de registros** no qual foram criados, mesmo que o mesmo comando seja usado. Isso significa que você não pode usar um **indicador** obtido de um **conjunto de registros** para mover para o mesmo registro em um segundo conjunto de **registros** aberto com o mesmo comando.
