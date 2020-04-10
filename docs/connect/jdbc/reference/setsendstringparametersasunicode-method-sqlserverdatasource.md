---
title: Método setSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9aa896cf8af60167bb1903002d292d48c2c476c9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924904"
---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>Método setSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **booliano** que indica se o envio de parâmetros de cadeia de caracteres ao servidor no formato UNICODE está habilitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sendStringParametersAsUnicode*  
  
 **true** se os parâmetros da cadeia de caracteres são enviados ao servidor no formato UNICODE. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade sendStringParametersAsUnicode for definida como **true**, que é o valor padrão, os parâmetros de cadeia de caracteres serão enviados ao servidor no formato UNICODE. Se a propriedade sendStringParametersAsUnicode for definida como **false**, os parâmetros de cadeia de caracteres serão enviados ao servidor em um formato ASCII/MBCS, e não em UNICODE. Se sendStringParametersAsUnicode não for definida, [getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) retornará o valor padrão, **true**.  
  
 Confira mais informações sobre a propriedade de conexão sendStringParametersAsUnicode, confira [Configuração das propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
