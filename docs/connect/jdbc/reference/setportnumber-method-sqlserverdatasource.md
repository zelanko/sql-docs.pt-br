---
title: Método setPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e0ff764637869428945ab3eb4b6c44b055b436
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728194"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>Método setPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número da porta a ser usada para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *portNumber*  
  
 Um valor **int** que contém o número da porta.  
  
## <a name="remarks"></a>Remarks  
 O número da porta é o número da porta TCP/IP usada ao abrir uma conexão de soquete com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade portNumber não estiver definida, o método [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) retornará o valor padrão de 1433.  
  
> [!NOTE]  
>  Método setPortNumber não faz qualquer intervalo de verificação no valor da porta transmitido. Você pode passar um número de porta que não é válido, como 99999, sem acionar a um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
