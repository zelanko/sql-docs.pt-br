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
ms.openlocfilehash: df27a5368dfea7f417fb84e2ebe38a8987165aec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979974"
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
  
## <a name="remarks"></a>Comentários  
 Se a propriedade sendStringParametersAsUnicode for definida como **true**, que é o valor padrão, os parâmetros de cadeia de caracteres serão enviados ao servidor no formato UNICODE. Se a propriedade sendStringParametersAsUnicode for definida como **false**, os parâmetros de cadeia de caracteres serão enviados ao servidor em um formato ASCII/MBCS, e não em UNICODE. Se sendStringParametersAsUnicode não for definida, getSendStringParametersAsUnicode retornará o valor padrão, **true**.  
  
 Confira mais informações sobre a propriedade de conexão sendStringParametersAsUnicode, confira [Configuração das propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
