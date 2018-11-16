---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e9f9a4e6af61eb507fa58f70b0aeb9060a16940
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605076"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera o valor de um atributo PDOStatement predefinido ou de um atributo de driver personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*attribute*: um inteiro, uma das constantes PDO::ATTR_* ou PDO::SQLSRV_ATTR_\*. Atributos com suporte são os atributos que podem ser definidas com [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md), PDO:: sqlsrv_attr_direct_query (para obter mais informações, consulte [execução de instrução direta e execução de instrução preparada no o Driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO:: attr_cursor e PDO:: sqlsrv_attr_cursor_scroll_type (para obter mais informações, consulte [tipos de Cursor (Driver PDO_SQLSRV)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>Valor retornado  
Em caso de sucesso, retorna um valor (misto) para um atributo PDO predefinido ou um atributo de driver personalizado. Retorna null em caso de falha.  
  
## <a name="remarks"></a>Remarks  
Consulte [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) para obter um exemplo.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
