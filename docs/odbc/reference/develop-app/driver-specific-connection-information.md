---
title: Informações de conexão específicas do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69f2c98678739a8b7879e152e13546f2bf9b9cc1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046936"
---
# <a name="driver-specific-connection-information"></a>Informações de conexão específicas de driver
O **SQLConnect** pressupõe que um nome de fonte de dados, ID de usuário e senha são suficientes para se conectar a uma fonte de dados e que todas as outras informações de conexão podem ser armazenadas no sistema. Esse geralmente não é o caso. Por exemplo, um driver pode precisar de uma ID de usuário e senha para fazer logon em um servidor e uma ID de usuário e senha diferentes para fazer logon em um DBMS. Como o **SQLConnect** aceita uma única ID de usuário e senha, isso significa que a outra ID de usuário e a senha devem ser armazenadas com as informações da fonte de dados no sistema se o **SQLConnect** for usado. Essa é uma possível violação de segurança e deve ser evitada a menos que a senha seja criptografada.  
  
 O **SQLDriverConnect** permite que o driver defina uma quantidade arbitrária de informações de conexão nos pares de palavra-chave-valor da cadeia de conexão. Por exemplo, suponha que um driver exija um nome de fonte de dados, uma ID de usuário e uma senha para o servidor e uma ID de usuário e senha para o DBMS. Um programa personalizado que sempre usa a fonte de dados corporativa XYZ pode solicitar ao usuário IDs e senhas e criar o seguinte conjunto de pares de palavra-chave-valor, ou *cadeia de conexão,* para passar para **SQLDriverConnect**:  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à `Trusted_Connection=yes` autenticação do Windows, especifique o lugar das informações de ID de usuário e senha na cadeia de conexão.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 A palavra-chave **DSN** (nome da fonte de dados) nomeia a fonte de dados, as palavras-chave **UID** e **pwd** especificam a ID de usuário e a senha do servidor, e as palavras-chave **UIDDBMS** e **PWDDBMS** especificam a ID de usuário e a senha para o DBMS. Observe que o ponto e vírgula final é opcional. **SQLDriverConnect** analisa essa cadeia de caracteres; usa o nome da fonte de dados corporativa XYZ para recuperar informações de conexão adicionais do sistema, como o endereço do servidor; e faz logon no servidor e no DBMS usando as IDs de usuário e as senhas especificadas.  
  
 Pares de palavra-chave-valor em **SQLDriverConnect** devem seguir determinadas regras de sintaxe. As palavras-chave e seus valores não devem conter o **[]{}(),;? = \*! @** caracteres. O valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco e não deve conter espaços em branco à esquerda. Devido à gramática do registro, as palavras-chave e os nomes de fonte de dados não podem\\conter o caractere de barra invertida (). Os espaços não são permitidos em relação ao sinal de igual no par de palavra-chave-valor.  
  
 A palavra-chave **FILEDSN** pode ser usada em uma chamada para **SQLDriverConnect** para especificar o nome de um arquivo que contém informações da fonte de dados (consulte [conectando-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), mais adiante nesta seção). A palavra-chave **SaveFile** pode ser usada para especificar o nome de um arquivo. DSN no qual os pares de palavra-chave-valor de uma conexão bem-sucedida feita pela chamada para **SQLDriverConnect** serão salvos. Para obter mais informações sobre fontes de dados de arquivo, consulte a descrição da função [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .
