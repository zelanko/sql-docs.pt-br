---
title: Usando indicadores | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cbabea62b99f36adb2adf9f12e52d80644f33ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-bookmarks"></a>Usando indicadores
Geralmente é útil retornar diretamente a um registro específico após ter movido **registros** sem a necessidade de percorrer cada registro e comparar valores. Por exemplo, se você tentar procurar um registro usando o **localizar** método, mas a pesquisa não retornou nenhum registro, são colocados automaticamente em ambas as extremidades do **registros**. Se o provedor oferece suporte a eles, indicadores podem ser usados para marcar o local antes de usar o **localizar** método para que você possa retornar para seu local. Um indicador é um **Variant** tipo de valor que identifica exclusivamente um registro em um **registros** objeto.  
  
 Você também pode usar uma matriz de variant de marcadores com o **filtro de conjunto de registros** método para filtrar em um conjunto de registros selecionado. Para obter detalhes sobre essa técnica, consulte filtrar os resultados no tópico [trabalhando com conjuntos de registros](../../../ado/guide/data/working-with-recordsets.md), mais adiante nesta seção.  
  
 Você pode usar o **indicador** para obter um indicador para um registro ou definir o registro atual um **registros** objeto para o registro identificado por um indicador válido. O código a seguir usa o **indicador** propriedade para definir um indicador e, em seguida, retornar para o registro indicado após passar para outros registros. Para determinar se seu **registros** dá suporte a indicadores, use o **suporta** método.  
  
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
  
 O [suporta](../../../ado/reference/ado-api/supports-method.md) método é abordado em mais detalhes posteriormente.  
  
 Exceto no caso de clonado **conjuntos de registros**, indicadores são exclusivos para o **registros** no qual eles foram criados, mesmo se o mesmo comando é usado. Isso significa que você não pode usar um **indicador** obtidas de um **registros** para mover para o mesmo registro em um segundo **registros** aberta com o mesmo comando.
