---
description: Parâmetro (ADO – Sintaxe WFC)
title: Parâmetro (ADO – sintaxe WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fc5226da0ceeefc6ae961b2a3d358d1dc1955b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442818"
---
# <a name="parameter-ado---wfc-syntax"></a>Parâmetro (ADO – Sintaxe WFC)
## <a name="package-commswfcdata"></a>pacote com. ms. wfc. Data  
  
### <a name="constructor"></a>Construtor  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>Métodos de acessador de parâmetro  
 A propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) de um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) Obtém ou define o conteúdo desse objeto. O conteúdo é representado como uma variante, um tipo de objeto que pode ser atribuído a um valor e qualquer um de vários tipos de dados.  
  
 O ADO/WFC implementa a propriedade **Value** com o método **GetValue** , que retorna um objeto Variant; e o método **SetValue** , que usa uma variante como um argumento. As VARIAntes são altamente eficientes em determinadas linguagens, como o Microsoft Visual Basic.  
  
 Além da propriedade **Value** , o ADO/WFC fornece métodos *acessadores* que usam tipos de dados Java para obter e definir o conteúdo dos objetos de **parâmetro** . A maioria desses métodos tem nomes do formulário **obter**_DataType_ ou **definir**_DataType_.  
  
 Há uma exceção notável: não há nenhuma propriedade **getnull** ; em vez disso, há uma propriedade **IsNull** que retorna um valor booliano que indica se o campo é nulo.  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
