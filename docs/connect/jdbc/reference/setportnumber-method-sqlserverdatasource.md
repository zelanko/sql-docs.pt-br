---
description: Método setPortNumber (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbf1cccfab3cef60193cc9b45921c203821cbfca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458478"
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
  
## <a name="remarks"></a>Comentários  
 O número da porta é o número da porta TCP/IP usada ao abrir uma conexão de soquete com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade portNumber não estiver definida, o método [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) retornará o valor padrão de 1433.  
  
> [!NOTE]  
>  O método setPortNumber não faz nenhuma verificação de intervalo no valor de porta passado. Você pode passar um número da porta que não é válido, como 99999, sem disparar nenhum erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
