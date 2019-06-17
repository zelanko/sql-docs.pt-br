---
title: Criar chaves simétricas idênticas em dois servidores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 85901ba63607de721259431ab83d3a0cd3a3185d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011717"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>Criar chaves simétricas idênticas em dois servidores
  Este tópico descreve como criar chaves simétricas idênticas em dois servidores diferentes no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para descriptografar texto cifrado, você precisa da chave que foi usada para criptografá-lo. Quando ocorrem criptografia e descriptografia em um único banco de dados, a chave é armazenada no banco de dados e fica disponível, dependendo das permissões, tanto para criptografia quanto para descriptografia. Mas quando a criptografia e a descriptografia ocorrem em bancos de dados ou servidores separados, a chave armazenada em um banco de dados não estará disponível para uso no segundo banco de dados  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para criar chaves simétricas idênticas em dois servidores diferentes, usando Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando uma chave simétrica é criada, a chave simétrica deve ser criptografada usando pelo menos um dos seguintes: senha, certificado, chave simétrica, chave assimétrica ou provedor. A chave pode ter mais de uma criptografia de cada tipo. Em outras palavras, uma única chave simétrica pode ser criptografada com o uso de vários certificados, senhas, chaves simétricas e chaves assimétricas ao mesmo tempo.  
  
-   Quando uma chave simétrica é criptografada com uma senha e não com a chave pública da chave mestre do banco de dados, o algoritmo de criptografia TRIPLE DES é usado. Por esse motivo, as chaves criadas com um algoritmo de criptografia forte, como AES, são protegidas por um algoritmo mais fraco.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer permissão ALTER ANY SYMMETRIC KEY no banco de dados. Se AUTHORIZATION for especificada, será necessária a permissão IMPERSONATE no usuário de banco de dados ou a permissão ALTER na função de aplicativo. Se a criptografia for por certificado ou chave assimétrica, exigirá a permissão VIEW DEFINITION no certificado ou na chave assimétrica. Somente logons do Windows, logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e funções de aplicativo podem ter chaves simétricas. Grupos e funções não podem possuir chaves simétricas.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>Para criar chaves simétricas idênticas em dois servidores diferentes  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Crie a chave executando as instruções CREATE MASTER KEY, CREATE CERTIFICATE e CREATE SYMMETRIC KEY.  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  Conecte a uma instância de servidor separada, abra uma Janela de Consulta diferente e execute as instruções SQL acima para criar a mesma chave no segundo servidor.  
  
5.  Teste as chaves executando primeiro a instrução OPEN e a instrução SELECT abaixo no primeiro servidor.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  No segundo servidor, cole o resultado da instrução SELECT anterior no seguinte código como o valor de `@blob` e execute esse código para verificar se a chave duplicada pode descriptografar o texto cifrado.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  Feche a chave simétrica em ambos os servidores.  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 Para obter mais informações, consulte o seguinte:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/decryptbykey-transact-sql)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-symmetric-key-transact-sql)  
  
  
