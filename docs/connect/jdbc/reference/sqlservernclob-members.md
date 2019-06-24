---
title: Membros SQLServerNClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8386d896391405777648ee3ec27b188b313c737c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66788960"
---
# <a name="sqlservernclob-members"></a>Membros SQLServerNClob
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhum.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[gratuito](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|Esse método libera o objeto **NCLOB** e os recursos que ele contém.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|Recupera o **NCLOB** valor designado pelo **NCLOB** objeto como um fluxo de ASCII.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|Recupera o **NCLOB** valor designado pelo **NCLOB** objeto.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|Recupera uma cópia da subcadeia de caracteres especificada na **NCLOB** valor designado pelo **NCLOB** objeto.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|Recupera o número de caracteres a **NCLOB** valor designado pelo **NCLOB** objeto.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|Recupera a posição do caractere do objeto **java.sql.NClob** ou da subcadeia de caracteres especificada no **java.sql.NClob** com base na posição inicial.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|Recupera um fluxo a ser usado para gravar caracteres ASCII no valor **NCLOB** que o objeto **java.sql.NClob** em questão representa, começando na posição especificada.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|Recupera um fluxo a ser usado para gravar um fluxo de caracteres Unicode no valor **NCLOB** que o objeto **java.sql.NClob** em questão representa, começando na posição especificada.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|Grava a especificada **cadeia de caracteres** para o **NCLOB** começando na posição especificada.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|Trunca o valor **NCLOB** no comprimento especificado.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de|Métodos|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
