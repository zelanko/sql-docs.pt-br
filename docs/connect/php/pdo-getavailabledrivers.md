---
title: PDO::getAvailableDrivers
description: Referência de API para a função PDO::getAvailableDrivers no Driver do Microsoft PDO_SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e43ef53820d24128d16ee0f0c7a5d6f1077ff6d2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646612"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna uma matriz dos drivers de PDO na sua instalação do PHP.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>Valor retornado  
Uma matriz com a lista de drivers de PDO.  
  
## <a name="remarks"></a>Comentários  
O nome do driver de PDO é usado em PDO::__construct para criar uma instância de PDO.  
  
Não é necessário implementar PDO::getAvailableDrivers por drivers do PHP. Para obter mais informações sobre esse método, consulte a documentação do PHP.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
