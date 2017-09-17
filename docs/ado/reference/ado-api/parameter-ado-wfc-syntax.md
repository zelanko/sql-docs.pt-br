---
title: "Parâmetro (ADO - sintaxe WFC) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7006bc7073693cc70dcb8eebce1bd8998895a9e8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-ado---wfc-syntax"></a>Parâmetro (ADO - WFC sintaxe)
## <a name="package-commswfcdata"></a>pacote com.ms.wfc.data  
  
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
 O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto obtém ou define o conteúdo do objeto. O conteúdo é representado como uma VARIANTE de um tipo de objeto que pode ser atribuído um valor e qualquer um dos vários tipos de dados.  
  
 ADO/WFC implementa o **valor** propriedade com o **getValue** método, que retorna um objeto de VARIANTE; e o **setValue** método, que usa uma VARIANTE como um argumento. Variantes são altamente eficientes em determinados idiomas, como o Microsoft Visual Basic.  
  
 Além de **valor** propriedade ADO/WFC fornece *acessador* métodos que usam tipos de dados Java para obter e definir o conteúdo de **parâmetro** objetos. A maioria desses métodos têm nomes no formato **obter***DataType* ou **definir***DataType*.  
  
 Há uma exceção notável: não há nenhum **getNull** propriedade; em vez disso, há um **isNull** propriedade que retorna um valor booliano que indica se o campo é nulo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
