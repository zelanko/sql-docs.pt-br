---
title: Método getSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88f5d294e46ddc6dc4da92e437fc4513f9a50a47
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792004"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>Método getSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se os parâmetros da cadeia de caracteres são enviados ao servidor no formato UNICODE. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade sendStringParametersAsUnicode for definida como **true**, que é o valor padrão, os parâmetros de cadeia de caracteres serão enviados ao servidor no formato UNICODE. Se a propriedade sendStringParametersAsUnicode for definida como **false**, os parâmetros de cadeia de caracteres serão enviados ao servidor em um formato ASCII/MBCS, e não em UNICODE. Se sendStringParametersAsUnicode não for definida, getSendStringParametersAsUnicode retornará o valor padrão, **true**.  
  
 Para obter mais informações sobre a propriedade de conexão sendStringParametersAsUnicode, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
