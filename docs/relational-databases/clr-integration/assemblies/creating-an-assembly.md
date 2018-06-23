---
title: Criando um Assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dda63f58c6229da4af2653d68d6bc7db37043e62
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694327"
---
# <a name="creating-an-assembly"></a>Criando um assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os objetos de banco de dados gerenciado, como os procedimentos armazenados ou gatilhos, são compilados e implantados em unidades chamadas de assembly. Os assemblies DLL gerenciados devem ser registrados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes da funcionalidade do assembly pode ser usada. Para registrar um assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use a instrução CREATE ASSEMBLY. Este tópico trata sobre como registrar um assembly em um banco de dados usando a instrução CREATE ASSEMBLY e como especificar as configurações de segurança do assembly.  
  
## <a name="the-create-assembly-statement"></a>A instrução CREATE ASSEMBLY  
 A instrução CREATE ASSEMBLY é usada para criar um assembly em um banco de dados. A seguir está um exemplo:  
  
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
 Ao criar um assembly em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados, você pode especificar um dos três diferentes níveis de segurança no qual seu código pode ser executado: **seguro**, **EXTERNAL_ACCESS**, ou **UNSAFE** . Quando o **CREATE ASSEMBLY** instrução é executada, determinadas verificações são realizadas no assembly de código que pode fazer com que o assembly não foi possível registrar no servidor. Para obter mais informações, consulte o exemplo de representação em [CodePlex](http://msftengprodsamples.codeplex.com/).  
  
 **SEGURANÇA** é o conjunto de permissões padrão e funciona para a maioria dos cenários. Para especificar um determinado nível de segurança, modifique a sintaxe da instrução CREATE ASSEMBLY da seguinte maneira:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 Também é possível criar um assembly com o **seguro** permissão definida simplesmente omitindo a terceira linha de código acima:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando o código em um assembly é executada sob o **seguro** permissão definido, ele só pode fazer cálculos e acessar dados no servidor por meio do provedor gerenciado em processo.  
  
### <a name="creating-externalaccess-and-unsafe-assemblies"></a>Criando assemblies EXTERNAL_ACCESS e UNSAFE  
 **EXTERNAL_ACCESS** abrange cenários em que o código precisa acessar recursos fora do servidor, como arquivos, rede, registro e variáveis de ambiente. Sempre que o servidor acessa um recurso externo, ele representa o contexto de segurança do usuário que chama o código gerenciado.  
  
 **UNSAFE** permissão de código é para essas situações em que um assembly não é verificável ou exige acesso adicional a recursos restritos, como o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] API do Win32.  
  
 Para criar um **EXTERNAL_ACCESS** ou **UNSAFE** assembly no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma das duas condições a seguir deve ser atendida:  
  
1.  O assembly é assinado com nome forte ou com Authenticode usando um certificado. Esse nome forte (ou certificado) é criado dentro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma chave assimétrica (ou certificado), e tem um logon correspondente com **EXTERNAL ACCESS ASSEMBLY** permissão (para assemblies de acesso externo) ou  **UNSAFE ASSEMBLY** permissão (para assemblies não seguros).  
  
2.  O proprietário do banco de dados (DBO) possui **EXTERNAL ACCESS ASSEMBLY** (para **acesso externo** assemblies) ou **UNSAFE ASSEMBLY** (para **UNSAFE** permissão de assemblies) e o banco de dados tem o [propriedade TRUSTWORTHY do banco de dados](../../../relational-databases/security/trustworthy-database-property.md) definida como **ON**.  
  
 As duas condições listadas acima também são verificadas na hora do carregamento do assembly (que inclui a execução). Pelo menos um das condições precisa ser cumprida para carregar o assembly.  
  
 É recomendável que o [propriedade TRUSTWORTHY do banco de dados](../../../relational-databases/security/trustworthy-database-property.md) em um banco de dados não será definido como **ON** apenas para executar o common language runtime (CLR) de código no processo do servidor. Em vez disso, recomendamos que seja criada uma chave assimétrica do arquivo de assembly no banco de dados mestre. Um logon mapeado para essa chave assimétrica deve ser criado e o logon deve ser concedido **EXTERNAL ACCESS ASSEMBLY** ou **UNSAFE ASSEMBLY** permissão.  
  
 O seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções executam as etapas necessárias para criar uma chave assimétrica, mapear um logon para essa chave e, em seguida, conceder **EXTERNAL_ACCESS** permissão ao logon. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
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
  
 Para criar um **acesso externo** assembly, o criador precisa ter **acesso externo** permissão. Isso é especificado ao criar o assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 O seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções executam as etapas necessárias para criar uma chave assimétrica, mapear um logon para essa chave e, em seguida, conceder **UNSAFE** permissão ao logon. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Para especificar que um assembly é carregado com **UNSAFE** permissão, especifique o **UNSAFE** conjunto de permissões ao carregar o assembly no servidor:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Para obter mais detalhes sobre as permissões para cada uma das configurações, consulte [CLR Integration Security](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando Assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Alterando um Assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Descartar um Assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [Segurança de acesso do código de integração de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [propriedade TRUSTWORTHY do banco de dados](../../../relational-databases/security/trustworthy-database-property.md)   
 [Permitindo chamadores parcialmente confiáveis](http://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
