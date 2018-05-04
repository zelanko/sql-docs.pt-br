---
title: Protegendo cadeias de caracteres de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 69ce8557-5260-4ea4-81b8-d0c5481f0868
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1cdacc1732a029e2bd5360952c41ff712993d7d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="securing-connection-strings"></a>Protegendo cadeias de conexão
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A proteção do acesso à fonte de dados é uma das metas mais importantes para ajudar a proteger um aplicativo. Para limitar o acesso à fonte de dados, você deve tomar precauções para ajudar a proteger informações sobre a conexão, como ID de usuário, senha e nome da fonte de dados. O armazenamento de uma ID de usuário e senha em texto sem formatação, como no código-fonte, apresenta um erro grave de segurança. Mesmo que você forneça uma versão compilada do código que contenha informações sobre ID de usuário e senha em uma fonte externa, o código compilado pode ser desmontado e a ID de usuário, exposta. Assim, é essencial que as informações críticas, como ID de usuário e senha, não estejam no código.  
  
 É altamente recomendável que você não armazene a senha com a URL de conexão no código-fonte do aplicativo. Em vez disso, considere o armazenamento da senha em um arquivo à parte que tenha acesso restrito. O acesso a esse arquivo pode ser concedido ao contexto no qual o aplicativo está em execução.  
  
 Outra abordagem é armazenar a senha criptografada em um arquivo. Certifique-se de que usar uma API de criptografia que não exija o armazenamento da chave em algum lugar e não derive da senha de um usuário. Por exemplo, você pode considerar o uso de pares de chaves públicas/privadas baseadas no certificado ou usar uma abordagem em que duas partes usam um protocolo de acordo chave (algoritmo Diffie-Hellman) para gerar chaves secretas idênticas para criptografia sem sequer precisar transmitir a chave secreta.  
  
 Se usar informações sobre a cadeia de conexão de uma fonte externa, como um usuário que forneça uma ID de usuário e senha, você deverá validar todas as entradas na fonte para garantir que elas tenham o formato correto e não contenham parâmetros adicionais que afetem a conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
