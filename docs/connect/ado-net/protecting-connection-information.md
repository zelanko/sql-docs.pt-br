---
title: Proteger informações de conexão
description: Saiba mais sobre vulnerabilidades de segurança em cadeias de conexão, que podem surgir devido à forma como as cadeias de conexão são construídas e persistidas e ao tipo de autenticação.
ms.date: 11/13/2020
ms.assetid: 1471f580-bcd4-4046-bdaf-d2541ecda2f4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 146063d665b89a8541c34d9cc3b0b6da3939d801
ms.sourcegitcommit: 7a3fdd3f282f634f7382790841d2c2a06c917011
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563092"
---
# <a name="protecting-connection-information"></a>Proteger informações de conexão

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A proteção do acesso à fonte de dados é essencial para a segurança do aplicativo. Uma cadeia de conexão apresenta uma vulnerabilidade potencial se não estiver protegida. Armazenar as informações de conexão em texto sem formatação ou persistir-la na memória pode comprometer seu sistema inteiro. As cadeias de conexão inseridas em seu código-fonte podem ser lidas usando o [Ildasm.exe (desmontador de IL)](/dotnet/framework/tools/ildasm-exe-il-disassembler) para exibir a MSIL (Microsoft Intermediate Language) em um assembly compilado.

As vulnerabilidades de segurança envolvendo cadeias de conexão podem surgir com base no tipo de autenticação usado, em como as cadeias de conexão são persistidas na memória e no disco e nas técnicas usadas para construí-los em tempo de execução.

## <a name="use-windows-authentication"></a>Usar Autenticação do Windows

Para ajudar a limitar o acesso a sua fonte de dados, você deverá proteger as informações de conexão como a identificação do usuário, senha e nome da fonte de dados. Para evitar expor as informações do usuário, recomendamos usar a autenticação do Windows (às vezes chamada de *segurança integrada*) sempre que for possível. A autenticação do Windows é especificada em uma cadeia de conexão usando as palavras-chave `Integrated Security` ou `Trusted_Connection`, eliminando a necessidade de usar uma identificação de usuário e senha. Ao usar a autenticação do Windows, os usuários são autenticados pelo Windows e o acesso ao servidor e os recursos de banco de dados são determinados concedendo permissões a usuários e grupos do Windows.

Para situações onde não é possível usar a autenticação do Windows, você deverá ter cuidado adicional porque as credenciais do usuário são expostas na cadeia de conexão. Em um aplicativo do ASP.NET, você pode configurar uma conta do Windows como uma identidade fixa que é usada para se conectar a bancos de dados e outros recursos de rede. Você habilita a representação no elemento de identidade no arquivo **web.config** e especifica um nome de usuário e uma senha.

```xml  
<identity impersonate="true"
        userName="MyDomain\UserAccount"
        password="*****" />  
```  

A conta de identidade fixa deve ser uma conta de privilégios baixos que tem concedidas somente as permissões necessárias no banco de dados. Além disso, você deve criptografar o arquivo de configuração de modo que o nome de usuário e a senha não sejam expostos em texto não criptografado.

## <a name="avoid-injection-attacks-with-connection-string-builders"></a>Evite ataques de injeção com construtores de cadeia de conexão

Um ataque de injeção de cadeia de conexão pode ocorrer quando a concatenação dinâmica de cadeia de caracteres é usada para criar cadeias de conexão com base na entrada do usuário. Se a entrada do usuário não for validada e o texto mal-intencionado ou caracteres não forem escapados, um invasor poderá acessar dados confidenciais ou outros recursos no servidor. Para resolver esse problema, o Provedor de Dados Microsoft SqlClient para SQL Server introduziu uma nova classe de construtor de cadeia de conexão para validar a sintaxe da cadeia de conexão e garantir que parâmetros adicionais não sejam introduzidos. Para obter mais informações, confira [Construtores de cadeias de conexão](connection-string-builders.md).

## <a name="use-persist-security-infofalse"></a>Use segurança de persistência Info=False

O valor padrão para `Persist Security Info` é falso; nós recomendamos usar esta opção em todas as cadeias de conexão. Configurar `Persist Security Info` como `true` ou `yes` permite informações confidenciais de segurança, incluindo a identificação de usuário e a senha, para serem obtidas de uma conexão depois que ela tiver sido aberta. Quando `Persist Security Info` for definido como `false` ou `no`, as informações de segurança serão descartadas após serem usadas para abrir a conexão, garantindo que uma fonte não confiável não tenha acesso a informações confidenciais de segurança.

## <a name="encrypt-configuration-files"></a>Criptografe arquivos de configuração

[!INCLUDE[appliesto-netfx-netcore-xxxx-md](../../includes/appliesto-netfx-netcore-xxxx-md.md)]

Você também pode armazenar cadeias de conexão em arquivos de configuração, o que elimina a necessidade de inseri-las no código do aplicativo. Os arquivos de configuração são arquivos XML padrão para os quais o .NET Framework definiu um conjunto comum de elementos. As cadeias de conexão em arquivos de configuração são geralmente armazenadas dentro do elemento **\<connectionStrings>** no **app.config** para um aplicativo do Windows ou no arquivo **web.config** para um aplicativo do ASP.NET. Para obter mais informações sobre noções básicas de armazenamento, recuperação e criptografia de cadeias de conexão de arquivos de configuração, confira [Cadeias de conexão e arquivos de configuração](connection-strings-and-configuration-files.md).

## <a name="see-also"></a>Confira também

- [Criptografar informações de configuração usando configuração protegida](/previous-versions/aspnet/53tyfkaw(v=vs.100)).
