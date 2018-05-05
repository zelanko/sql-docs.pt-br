---
title: PDO::getAvailableDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 251d81d568f3ade2a843d3288cb9bc92fdb8bc41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna uma matriz dos drivers de PDO na sua instalação do PHP.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz com a lista de drivers de PDO.  
  
## <a name="remarks"></a>Remarks  
O nome do driver de PDO é usado em PDO::__construct para criar uma instância de PDO.  
  
Não é necessário implementar PDO::getAvailableDrivers por drivers do PHP. Para obter mais informações sobre esse método, consulte a documentação do PHP.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
