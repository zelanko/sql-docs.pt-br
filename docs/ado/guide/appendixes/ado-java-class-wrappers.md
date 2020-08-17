---
description: Wrappers de classe Java ADO
title: Wrappers de classe Java ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: rothja
ms.author: jroth
ms.openlocfilehash: c02865fc20d741fc8b3f80ccecd56fcb105ad45e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355212"
---
# <a name="ado-java-class-wrappers"></a>Wrappers de classe Java ADO
Esse código declara uma instância do wrapper da classe ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) e a inicializa, tudo na mesma linha de código. Além disso, ele declara variáveis para cada um dos argumentos no método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) , especialmente para [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) e [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (porque Java não dá suporte a tipos enumerados). Ele é aberto e fecha o objeto **Recordset** . A definição de RS1 como NULL simplesmente agenda essa variável para ser liberada quando o Java executa sua versão sistemática e intermitente de objetos não utilizados.  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usando o Microsoft SDK para Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
