---
title: 'Coleções (Visual C++ índice de sintaxe com #import) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fa18eeacad58195c42d03b12f03332c332b0a35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662654"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>Coleções (Visual C++ índice de sintaxe com #import)
É útil saber que as coleções herdam certos métodos e propriedades comuns.  
  
 Todas as coleções de herdam a **contagem** propriedade e **atualizar** método e todas as coleções, adicione o **Item** propriedade. O **erros** coleção adiciona as **clara** método. O **parâmetros** herda de coleção de **Append** e **excluir** métodos, enquanto o **campos** coleção adiciona o **Append**, **excluir**, e **atualização** métodos.  
  
## <a name="properties-collection"></a>Coleção de propriedades  
  
### <a name="methods"></a>Métodos  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>Coleção de erros  
  
### <a name="methods"></a>Métodos  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Coleção Parâmetros  
  
### <a name="methods"></a>Métodos  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Coleção Campos  
  
### <a name="methods"></a>Métodos  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>Consulte também  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
