---
description: Autenticação de certificado do cliente para cenários de loopback
title: Autenticação de certificado do cliente para cenários de loopback | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: peterbae
ms.author: v-hyba
ms.openlocfilehash: bfc8816c30020669918b3632f94e289524097537
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438438"
---
# <a name="client-certificate-authentication-for-loopback-scenarios"></a>Autenticação de certificado do cliente para cenários de loopback

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um novo procedimento armazenado chamado SPEES (sp_execute_external_script) foi adicionado ao SQL Server 2016. Esse procedimento permite que o SQL Server inicie e execute um script externo fora da plataforma, como parte de um esforço de extensibilidade. Com ele, veio o suporte para scripts do R e do Python, ambos com bibliotecas que podem usar um JDBC Driver para se conectar ao SQL Server. Embora o SQL Server na caixa do Windows possa usar a Autenticação Integrada do Windows para autenticar essas conexões de loopback com as mesmas credenciais que o usuário que iniciou a consulta, o Linux SQL Server não pode fazer o mesmo. Portanto, a autenticação de certificado do cliente está sendo adicionada para permitir que os usuários autentiquem com um certificado e uma chave.

## <a name="connecting-using-client-certificate-authentication"></a>Conectar usando a Autenticação de certificado do cliente

O JDBC Driver adiciona três propriedades de conexão a esse recurso:

* clientCertificate – especifica o certificado a ser usado para autenticação. O JDBC Driver dará suporte às extensões de arquivo PFX, PEM, DER e CER.

Formatar
```
clientCertificate=<file_location>
``` 
O driver usa um arquivo de certificado. Para certificados nos formatos PEM, DER e CER, o atributo clientKey é exigido. A localização do arquivo pode ser relativa ou absoluta.
 
* clientKey – especifica uma localização de arquivo da chave privada para certificados PEM, DER ou CER especificados pelo atributo clientCertificate.

Formatar
```
clientKey=<file_location>
```
Especifica o local do arquivo de chave privada. Caso o arquivo de chave privada seja protegido por senha, a palavra-chave da senha será exigida. A localização do arquivo pode ser relativa ou absoluta.

* clientKeyPassword – cadeia de caracteres de senha opcional fornecida para acessar a chave privada do arquivo clientKey.

Esse recurso tem suporte oficial em cenários de autenticação de loopback no Linux SQL Server 2019 e posterior.

## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
