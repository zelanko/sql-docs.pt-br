---
title: Criando uma Montagem | Microsoft Docs
description: Use CREATE ASSEMBLY para registrar um conjunto no SQL Server e especificar suas configurações de segurança. Registre um conjunto para usar sua funcionalidade.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ca6787abae22722a7bbb99d335e63d47051bb46
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486825"
---
# <a name="creating-an-assembly"></a>Criando um assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os objetos de banco de dados gerenciado, como os procedimentos armazenados ou gatilhos, são compilados e implantados em unidades chamadas de assembly. Os conjuntos dll gerenciados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devem ser registrados antes que a funcionalidade que o conjunto fornece possa ser usada. Para registrar um assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use a instrução CREATE ASSEMBLY. Este tópico trata sobre como registrar um assembly em um banco de dados usando a instrução CREATE ASSEMBLY e como especificar as configurações de segurança do assembly.  
  
## <a name="the-create-assembly-statement"></a>A instrução CREATE ASSEMBLY  
 A instrução CREATE ASSEMBLY é usada para criar um assembly em um banco de dados. Veja um exemplo:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 A cláusula FROM especifica o nome do caminho do assembly a ser criado. Esse caminho pode ser um caminho UNC (convenção de nomenclatura universal) ou um caminho físico do arquivo que é local no computador.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não permite o registro de versões diferentes de um assembly com nome, cultura e chave pública iguais.  
  
 É possível criar assemblies que referenciem outros. Quando um assembly é criado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também cria os assemblies referenciados pelo assembly do nível raiz, se eles ainda não foram criados no banco de dados.  
  
 Os usuários de banco de dados ou as funções de usuário obtêm permissões para criar, e assim ter propriedade sobre, os assemblies em um banco de dados. Para criar assemblies, a função ou o usuário de banco de dados deve ter a permissão CREATE ASSEMBLY.  
  
 Um assembly só poderá ter êxito ao referenciar outros assemblies se:  
  
-   O assembly chamado ou referenciado tem como proprietário o mesmo usuário ou função.  
  
-   O assembly chamado ou referenciado foi criado no mesmo banco de dados.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Especificando a segurança ao criar assemblies  
 Ao criar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto em um banco de dados, você pode especificar um dos três níveis diferentes de segurança em que seu código pode ser executado: **SAFE,** **EXTERNAL_ACCESS**ou **UNSAFE**. Quando a declaração **CREATE ASSEMBLY** é executada, certas verificações são realizadas no conjunto de códigos, o que pode fazer com que o conjunto não se registre no servidor. Para obter mais informações, consulte a amostra de personificação no [CodePlex](https://msftengprodsamples.codeplex.com/).  
  
 **SAFE** é o conjunto de permissões padrão e funciona para a maioria dos cenários. Para especificar um determinado nível de segurança, modifique a sintaxe da instrução CREATE ASSEMBLY da seguinte maneira:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 Também é possível criar um conjunto com a permissão **SAFE** definida simplesmente omitindo a terceira linha de código acima:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando o código em um conjunto é executado sob o conjunto de permissões **SAFE,** ele só pode fazer o acesso à computação e aos dados dentro do servidor através do provedor gerenciado em processo.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Criando assemblies EXTERNAL_ACCESS e UNSAFE  
 **EXTERNAL_ACCESS** aborda cenários em que o código precisa acessar recursos fora do servidor, como arquivos, rede, registro e variáveis de ambiente. Sempre que o servidor acessa um recurso externo, ele representa o contexto de segurança do usuário que chama o código gerenciado.  
  
 A permissão de código **INSEGURA** é para aquelas situações em que um conjunto [!INCLUDE[msCoName](../../../includes/msconame-md.md)] não é verificávelmente seguro ou requer acesso adicional a recursos restritos, como a API Win32.  
  
 Para criar uma montagem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **EXTERNAL_ACCESS** ou **INSEGURA** em, uma das duas condições seguintes deve ser cumprida:  
  
1.  O assembly é assinado com nome forte ou com Authenticode usando um certificado. Este nome forte (ou certificado) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é criado no interior como uma chave assimétrica (ou certificado), e tem um login correspondente com permissão **DE MONTAGEM DE ACESSO EXTERNO** (para conjuntos de acesso externo) ou permissão DE MONTAGEM **INSEGURA** (para conjuntos inseguros).  
  
2.  O proprietário do banco de dados (DBO) tem a permissão **EXTERNAL ACCESS ASSEMBLY** (para conjuntos de acesso **externo)** ou **INSEGURA** ASSEMBLY (para conjuntos **inseguros)** e o banco de dados tem a [propriedade de banco de dados confiável](../../../relational-databases/security/trustworthy-database-property.md) definida como **ON**.  

 As duas condições listadas acima também são verificadas na hora do carregamento do assembly (que inclui a execução). Pelo menos um das condições precisa ser cumprida para carregar o assembly.  
  
 Recomendamos que a [propriedade de banco de dados confiável](../../../relational-databases/security/trustworthy-database-property.md) em um banco de dados não seja definida como **ON** apenas para executar o código CLR (Common Language Runtime, tempo de execução do idioma comum) no processo do servidor. Em vez disso, recomendamos que seja criada uma chave assimétrica do arquivo de assembly no banco de dados mestre. Um login mapeado para esta chave assimétrica deve ser criado e o login deve ser concedido **A MONTAGEM DE ACESSO EXTERNO** ou permissão DE MONTAGEM **INSEGURA.**  
  
 As [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções a seguir executam as etapas necessárias para criar uma chave assimétrica, mapear um login para essa chave e, em seguida, conceder **EXTERNAL_ACCESS** permissão para o login. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  Você deve criar um logon novo para associar com a chave assimétrica. Esse logon é usado somente para conceder permissões; não precisa estar associado a um usuário ou usado dentro do aplicativo.  
  
 Para criar um **conjunto EXTERNAL ACCESS,** o criador precisa ter permissão **DE ACESSO EXTERNO.** Isso é especificado ao criar o assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 As [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções a seguir executam as etapas necessárias para criar uma chave assimétrica, mapear um login para essa chave e, em seguida, conceder permissão **INSEGURA** para o login. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Para especificar que um conjunto carrega com permissão **INSEGURA,** você especifica o conjunto de permissões **INSEGURAS** ao carregar o conjunto no servidor:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Para obter mais detalhes sobre as permissões para cada uma das configurações, consulte [CLR Integration Security](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de Conjuntos de Integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Alterando uma Assembléia](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Soltando uma Assembléia](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [Segurança de acesso ao código de integração clr](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Propriedade confiável do banco de dados](../../../relational-databases/security/trustworthy-database-property.md)   
 [Permitindo chamadores parcialmente confiáveis](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
