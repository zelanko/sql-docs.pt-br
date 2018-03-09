---
title: "Informações de Conexão específicos de driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3352a0a31e6bb48be84d72a7da84eb3d7c6100c9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="driver-specific-connection-information"></a>Informações de Conexão específicos de driver
**SQLConnect** supõe que um nome de fonte de dados, ID de usuário e senha são suficientes para se conectar a uma fonte de dados e que todas as outras informações de conexão podem ser armazenadas no sistema. Isso frequentemente não for o caso. Por exemplo, um driver talvez seja necessário uma ID de usuário e senha para fazer logon um servidor e um ID de usuário diferente e uma senha para fazer logon um DBMS. Porque **SQLConnect** aceita um ID de usuário único e uma senha, isso significa que a ID de usuário e senha devem ser armazenados com as informações de fonte de dados do sistema se **SQLConnect** deve ser usado. Essa é uma possível violação de segurança e deve ser evitada, a menos que a senha é criptografada.  
  
 **SQLDriverConnect** permite que o driver definir uma quantidade arbitrária de informações de conexão nos pares de valor de palavra-chave da cadeia de caracteres de conexão. Por exemplo, suponha que um driver requer um nome de fonte de dados, uma ID de usuário e senha para o servidor e uma ID de usuário e senha para o DBMS. Um programa personalizado que sempre usa a fonte de dados XYZ Corp pode solicitar que o usuário IDs e senhas e criar o seguinte conjunto de pares de valor de palavra-chave, ou *cadeia de caracteres de conexão,* para passar para **SQLDriverConnect**:  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar `Trusted_Connection=yes` em vez das informações de ID e a senha do usuário na cadeia de conexão.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 O **DSN** palavra-chave (nome de fonte de dados) nomeia a fonte de dados, o **UID** e **PWD** palavras-chave especificam a ID de usuário e senha para o servidor e o **UIDDBMS**  e **PWDDBMS** palavras-chave especificam a ID de usuário e senha para o DBMS. Observe que o ponto e vírgula final é opcional. **SQLDriverConnect** analisa essa cadeia de caracteres; usa o nome de fonte de dados XYZ Corp para recuperar informações de conexão adicionais do sistema, como o endereço do servidor; e faça logon no servidor e DBMS usando as IDs de usuário especificada e senhas.  
  
 Pares de valor de palavra-chave no **SQLDriverConnect** devem seguir determinadas regras de sintaxe. As palavras-chave e seus valores não devem conter o **[] {} (),? \*=! @** caracteres. O valor de **DSN** palavra-chave não pode consistir apenas de espaços em branco e não deve conter espaços em branco à esquerda. Devido a gramática do registro, nomes de fontes de dados e palavras-chave não podem conter uma barra invertida (\\) caracteres. Não são permitidos espaços em torno do sinal de igual do par de valor de palavra-chave.  
  
 O **FILEDSN** palavra-chave pode ser usado em uma chamada para **SQLDriverConnect** para especificar o nome de um arquivo que contém informações de fonte de dados (consulte [se conectar usando o arquivo de fontes de dados](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), mais adiante nesta seção). O **SAVEFILE** palavra-chave pode ser usado para especificar o nome de um arquivo. DSN em que os pares de valor de palavra-chave de uma conexão bem-sucedida feitas pela chamada para **SQLDriverConnect** será salvo. Para obter mais informações sobre fontes de dados de arquivo, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.
