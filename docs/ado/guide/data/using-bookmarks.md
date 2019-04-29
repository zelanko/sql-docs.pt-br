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
manager: craigg
ms.openlocfilehash: a083f9d411474769335fdfae32bd59dfe455a9f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184927"
---
# <a name="using-bookmarks"></a>Usar indicadores
Geralmente é útil retornar diretamente a um registro específico após ter movidos a **Recordset** sem precisar rolar por todos os registros e comparar valores. Por exemplo, se você tentar procurar um registro usando o **encontrar** método, mas a pesquisa não retornar nenhum registro, são colocados automaticamente no final o **conjunto de registros**. Se seu provedor oferecer suporte a eles, os indicadores podem ser usados para marcar seu lugar antes de usar o **localizar** método para que você possa retornar para seu local. Um indicador é um **Variant** tipo de valor que identifica exclusivamente um registro em um **Recordset** objeto.  
  
 Você também pode usar uma matriz de variantes de marcadores com o **filtro de conjunto de registros** método para filtrar em um conjunto de registros selecionado. Para obter detalhes sobre essa técnica, consulte Filtrando os resultados no tópico [trabalhando com conjuntos de registros](../../../ado/guide/data/working-with-recordsets.md), mais adiante nesta seção.  
  
 Você pode usar o **indicador** propriedade para obter um indicador para um registro ou definir o registro atual um **Recordset** objeto para o registro identificado por um indicador válido. O código a seguir usa o **indicador** propriedade para definir um indicador e, em seguida, retornar para o registro com indicador depois de passar para outros registros. Para determinar se sua **conjunto de registros** dá suporte a indicadores, use o **dá suporte a** método.  
  
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
  
 O [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método é abordado em mais detalhes posteriormente.  
  
 Exceto para o caso de clonado **conjuntos de registros**, os indicadores são exclusivos para o **Recordset** no qual eles foram criados, mesmo se o mesmo comando é usado. Isso significa que você não pode usar um **indicador** obtidas de um **conjunto de registros** mover para o mesmo registro em um segundo **Recordset** aberta com o mesmo comando.
