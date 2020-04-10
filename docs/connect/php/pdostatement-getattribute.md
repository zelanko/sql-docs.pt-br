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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a401cded16dc139e5efc70129ceb0d66fd68dcd6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923454"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera o valor de um atributo PDOStatement predefinido ou de um atributo de driver personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>parâmetros  
$*attribute*: um inteiro, uma das constantes PDO::ATTR_* ou PDO::SQLSRV_ATTR_\*. Atributos compatíveis são os aqueles que você pode definir com [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), PDO::SQLSRV_ATTR_DIRECT_QUERY (para obter mais informações, veja [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO::ATTR_CURSOR e PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE (para obter mais informações, veja [Tipos de cursor [Driver PDO_SQLSRV]](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>Valor retornado  
Em caso de sucesso, retorna um valor (misto) para um atributo PDO predefinido ou um atributo de driver personalizado. Retorna null em caso de falha.  
  
## <a name="remarks"></a>Comentários  
Consulte [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) para obter um exemplo.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
