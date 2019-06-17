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
manager: jroth
ms.openlocfilehash: 304d63f7822990c4d8e4a9c0787c9e688c222580
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799631"
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
  
  
