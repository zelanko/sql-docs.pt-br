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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305779"
---
# <a name="driver-specific-connection-information"></a>Informações de conexão específicas de driver
**O SQLConnect** assume que um nome de origem de dados, iD de usuário e senha são suficientes para se conectar a uma fonte de dados e que todas as outras informações de conexão podem ser armazenadas no sistema. Isso não é o caso. Por exemplo, um driver pode precisar de um ID de usuário e senha para fazer logon em um servidor e um ID de usuário diferente e senha para fazer logon em um DBMS. Como **o SQLConnect** aceita um único ID de usuário e senha, isso significa que o outro ID e senha do usuário devem ser armazenados com as informações de origem de dados no sistema se o **SQLConnect** for usado. Esta é uma possível violação de segurança e deve ser evitada a menos que a senha seja criptografada.  
  
 **O SQLDriverConnect** permite que o driver defina uma quantidade arbitrária de informações de conexão nos pares de valor de palavra-chave da seqüência de conexão. Por exemplo, suponha que um driver exija um nome de origem de dados, um ID de usuário e senha para o servidor, e um ID de usuário e senha para o DBMS. Um programa personalizado que sempre usa a fonte de dados da XYZ Corp pode solicitar ao usuário iDs e senhas e criar o seguinte conjunto de pares de valor de palavra-chave, ou *seqüência de conexão,* para passar para **SQLDriverConnect**:  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de origem `Trusted_Connection=yes` de dados que suporta a autenticação do Windows, você deve especificar, em vez de Informações de ID do usuário e senha na seqüência de conexões.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 A palavra-chave **DSN** (Nome da Fonte de Dados) nomeia a fonte de dados, as palavras-chave **UID** e **PWD** especificam o ID e a senha do usuário para o servidor, e as palavras-chave **UIDDBMS** e **PWDDBMS** especificam o ID do usuário e a senha para o DBMS. Observe que o ponto e vírgula final é opcional. **O SQLDriverConnect** analisa esta seqüência; usa o nome de origem de dados da XYZ Corp para recuperar informações adicionais de conexão do sistema, como o endereço do servidor; e faz logon no servidor e no DBMS usando os IDs e senhas de usuário especificados.  
  
 Os pares de valor de palavras-chave no **SQLDriverConnect** devem seguir certas regras de sintaxe. As palavras-chave e seus valores não devem conter o **[];?{} \*=@personagens.** O valor da palavra-chave **DSN** não pode consistir apenas em espaços em branco e não deve conter espaços em branco. Devido à gramática do registro, palavras-chave e nomes\\de fonte de dados não podem conter o caractere barra invertida ( ). Os espaços não são permitidos em torno do sinal igual no par de valor de palavra-chave.  
  
 A palavra-chave **FILEDSN** pode ser usada em uma chamada para **SQLDriverConnect** para especificar o nome de um arquivo que contém informações de origem de dados (consulte [Conectando usando fontes de dados de arquivo,](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)mais tarde nesta seção). A palavra-chave **SAVEFILE** pode ser usada para especificar o nome de um arquivo .dsn no qual os pares de valor de palavra-chave de uma conexão bem-sucedida feita pela chamada ao **SQLDriverConnect** serão salvos. Para obter mais informações sobre fontes de dados de arquivos, consulte a descrição da função [SQLDriverConnect.](../../../odbc/reference/syntax/sqldriverconnect-function.md)
