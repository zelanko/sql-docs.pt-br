---
title: Campo (sintaxe ADO-WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583e6de7dc8c3ea05d61dda53c3e630d05e4d5f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918755"
---
# <a name="field-ado---wfc-syntax"></a>Campo (ADO – Sintaxe WFC)
## <a name="package-commswfcdata"></a>pacote com. ms. wfc. Data  
  
### <a name="methods"></a>Métodos  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (Para obter mais informações, consulte a documentação da interface com. ms. wfc. Data. IDataFormat.)  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>Métodos de acessador de campo  
 A propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) de um objeto [Field](../../../ado/reference/ado-api/field-object.md) Obtém ou define o conteúdo desse objeto. O conteúdo é representado como uma variante, um tipo de objeto que pode ser atribuído a um valor e qualquer um de vários tipos de dados.  
  
 O ADO/WFC implementa a propriedade **Value** com o método **GetValue** , que retorna um objeto Variant; e o método **SetValue** , que usa uma variante como um argumento. As VARIAntes são altamente eficientes em determinadas linguagens, como o Microsoft Visual Basic.  
  
 Além da propriedade **Value** , o ADO/WFC fornece métodos *acessadores* que usam tipos de dados Java para obter e definir o conteúdo de objetos de **campo** . A maioria desses métodos tem nomes do formulário **obter**_DataType_ ou **definir**_DataType_.  
  
 Há duas exceções notáveis: um dos métodos **GetObject** retorna um objeto forçado a uma classe especificada. Não há nenhuma propriedade **getnull** ; em vez disso, há uma propriedade **IsNull** que retorna um valor booliano que indica se o campo é nulo.  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)
