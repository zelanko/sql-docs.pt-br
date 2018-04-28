---
title: Método setPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 777493f356306fcb2adad1a1066795246e5a71ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setportnumber-method-sqlserverdatasource"></a>Método setPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número da porta a ser usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Número da porta*  
  
 Um **int** valor que contém o número da porta.  
  
## <a name="remarks"></a>Remarks  
 O número da porta é o número da porta TCP/IP que é usado ao abrir uma conexão de soquete para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se a propriedade portNumber não for definida, o [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) método retornará o valor padrão de 1433.  
  
> [!NOTE]  
>  O método setPortNumber não faz qualquer intervalo de verificação no valor da porta transmitido. Você pode passar um número de porta não é válido, como 99999, sem disparar um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
