---
title: PDO::__construct
description: Referência de API para a função PDO::__construct no Driver do Microsoft PDO_SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a815f72ef466442c601d0720243f9476a0cfc95
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081665"
---
# <a name="pdo__construct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cria uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$dsn*: uma cadeia de caracteres que contém o nome do prefixo (sempre `sqlsrv`), dois-pontos e a palavra-chave do servidor. Por exemplo, `"sqlsrv:server=(local)"`. Opcionalmente, você pode especificar outras palavras-chave de conexão. Consulte [Connection Options](../../connect/php/connection-options.md) para obter uma descrição da palavra-chave do servidor e das outras palavras-chave de conexão. O *$dsn* inteiro é incluído entre aspas; portanto, não se deve incluir cada palavra-chave de conexão entre aspas individualmente.  
  
*$username*: Opcional. Uma cadeia de caracteres que contém o nome do usuário. Para conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique a ID de logon. Para conectar usando a Autenticação do Windows, especifique `""`.  
  
*$password*: opcional. Uma cadeia de caracteres que contém a senha do usuário. Para conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique a senha. Para conectar usando a Autenticação do Windows, especifique `""`.  
  
*$driver_options*: Opcional. Você pode especificar atributos do Gerenciador de Driver do PDO e atributos específicos do driver dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] – PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ATTR_DIRECT_QUERY. Um atributo inválido não gerará uma exceção. Atributos inválidos geram exceções quando são especificados com [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
## <a name="return-value"></a>Valor de retorno  
Retorna um objeto PDO. Se ocorrer uma falha, retornará um objeto PDOException.  
  
## <a name="exceptions"></a>Exceções  
PDOException  
  
## <a name="remarks"></a>Comentários  
Você pode fechar um objeto de conexão definindo a instância como null.  
  
Após uma conexão, PDO::errorCode exibe 01000 em vez de 00000.  
  
Se PDO::__construct falhar por algum motivo, uma exceção será gerada, mesmo se PDO::ATTR_ERRMODE for definido como PDO::ERRMODE_SILENT.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example-with-database"></a>Exemplo com banco de dados  
Este exemplo mostra como se conectar a um servidor usando a Autenticação do Windows e especificar um banco de dados.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example-without-database"></a>Exemplo sem banco de dados  
Este exemplo mostra como se conectar a um servidor, especificando o banco de dados posteriormente.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
