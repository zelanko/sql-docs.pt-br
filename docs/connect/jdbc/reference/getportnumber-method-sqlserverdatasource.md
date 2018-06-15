---
title: Método getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61ac4328c0a1da1229e568de52cc2d2c89cec437
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836751"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o número da porta atual que é usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que contém o número da porta atual.  
  
## <a name="remarks"></a>Remarks  
 O número da porta é o número da porta TCP/IP que é usado ao abrir uma conexão de soquete para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se a propriedade portNumber não estiver definida, o método getPortNumber retornará o valor padrão de 1433.  
  
> [!NOTE]  
>  O [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) método não faz qualquer intervalo de verificação no valor da porta transmitido. Você pode transmitir números de porta que não são válidos, como 99999, sem disparar um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
