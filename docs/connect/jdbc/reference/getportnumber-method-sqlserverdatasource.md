---
title: Método getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fcd2c1260ee69cbd3a50573f53b07bf429da402
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925237"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o número da porta atual usada para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que contém o número da porta atual.  
  
## <a name="remarks"></a>Comentários  
 O número da porta é o número da porta TCP/IP usada ao abrir uma conexão de soquete com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade portNumber não estiver definida, o método getPortNumber retornará o valor padrão de 1433.  
  
> [!NOTE]  
>  O [método setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) não faz nenhuma verificação de intervalo no valor de porta passado. Você pode passar números de porta não válidos, como 99999, sem disparar nenhum erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
