---
title: PDO::__construct | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 71404af3dfbcc0599d53bdb719f4150c77cac332
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cria uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$dsn*: uma cadeia de caracteres que contém o nome do prefixo (sempre `sqlsrv`), dois-pontos e a palavra-chave do servidor. Por exemplo, `"sqlsrv:server=(local)"`. Opcionalmente, você pode especificar outras palavras-chave de conexão. Consulte [Connection Options](../../connect/php/connection-options.md) para obter uma descrição da palavra-chave do servidor e das outras palavras-chave de conexão. O *$dsn* inteiro é incluído entre aspas; portanto, não se deve incluir cada palavra-chave de conexão entre aspas individualmente.  
  
*$username*: opcional. Uma cadeia de caracteres que contém o nome do usuário. Para conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , especifique a ID de logon. Para conectar usando a Autenticação do Windows, especifique `""`.  
  
*$password*: opcional. Uma cadeia de caracteres que contém a senha do usuário. Para conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , especifique a senha. Para conectar usando a Autenticação do Windows, especifique `""`.  
  
*$driver_options*: opcional. Você pode especificar atributos do Gerenciador de Driver do PDO e [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] atributos específicos do driver – PDO:: sqlsrv_attr_encoding, PDO:: sqlsrv_attr_direct_query. Um atributo inválido não gerará uma exceção. Atributos inválidos geram exceções quando são especificados com [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
## <a name="return-value"></a>Valor de retorno  
Retorna um objeto PDO. Se ocorrer uma falha, retornará um objeto PDOException.  
  
## <a name="exceptions"></a>Exceções  
PDOException  
  
## <a name="remarks"></a>Comentários  
Você pode fechar um objeto de conexão definindo a instância como null.  
  
Após uma conexão, PDO::errorCode exibirá 01000 em vez de 00000.  
  
Se PDO::__construct falhar por algum motivo, uma exceção será gerada, mesmo se PDO::ATTR_ERRMODE for definido como PDO::ERRMODE_SILENT.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
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
  
## <a name="example"></a>Exemplo  
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
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

