---
title: Campo (ADO – sintaxe WFC) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ea2245c3f57b5ad3b14847f15791575afde1043c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537148"
---
# <a name="field-ado---wfc-syntax"></a>Campo (ADO – Sintaxe WFC)
## <a name="package-commswfcdata"></a>pacote com.ms.wfc.data  
  
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
  
 (Para obter mais informações, consulte a documentação para a interface com.ms.wfc.data.IDataFormat).  
  
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
 O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade de uma [campo](../../../ado/reference/ado-api/field-object.md) objeto obtém ou define o conteúdo desse objeto. O conteúdo é representado como uma VARIANTE, um tipo de objeto que pode ser atribuído um valor e qualquer um dos vários tipos de dados.  
  
 ADO/WFC implementa o **valor** propriedade com o **getValue** método, que retorna um objeto de VARIANTE; e o **setValue** método, que usa uma VARIANTE como um argumento. Variantes são altamente eficientes em determinados idiomas, como o Microsoft Visual Basic.  
  
 Além de **valor** propriedade, ADO/WFC fornece *acessador* métodos que usam tipos de dados Java para obter e definir o conteúdo de **campo** objetos. A maioria desses métodos têm nomes no formato **Obtenha**_DataType_ ou **definir**_DataType_.  
  
 Há duas exceções notáveis: Um dos **getObject** métodos retorna um objeto forçado em uma classe especificada. Não há nenhuma **getNull** propriedade; em vez disso, há um **isNull** propriedade que retorna um valor booliano que indica se o campo é nulo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
