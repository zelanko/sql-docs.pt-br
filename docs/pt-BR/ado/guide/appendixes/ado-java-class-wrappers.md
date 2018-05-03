---
title: Wrappers de classe Java ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d1ac9d3421aac0847782766bfc30d15f045abc9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ado-java-class-wrappers"></a>Wrappers de classe Java ADO
Esse código declara uma instância do ADO [registros](../../../ado/reference/ado-api/recordset-object-ado.md) wrapper de classe e a inicializa todos na mesma linha de código. Além disso, ele declara variáveis para cada um dos argumentos no [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método, especialmente para [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) e [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (porque não dá suporte ao Java enumerados tipos). Ele abre e fecha o **registros** objeto. Definir Rs1 como NULL simplesmente agenda essa variável para ser liberado quando Java executa a versão intermitente e sistemática de objetos não utilizados.  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Microsoft SDK para Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
