---
title: Criar chaves simétricas idênticas em dois servidores | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7158694719e11cca4ea355c5fe3b94359e00b952
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66428826"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>Criar chaves simétricas idênticas em dois servidores
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como criar chaves simétricas idênticas em dois servidores diferentes no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para descriptografar texto cifrado, você precisa da chave que foi usada para criptografá-lo. Quando ocorrem criptografia e descriptografia em um único banco de dados, a chave é armazenada no banco de dados e fica disponível, dependendo das permissões, tanto para criptografia quanto para descriptografia. Mas quando a criptografia e a descriptografia ocorrem em bancos de dados ou servidores separados, a chave armazenada em um banco de dados não estará disponível para uso no segundo banco de dados.
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
  
- Quando uma chave simétrica é criada, a chave simétrica deve ser criptografada usando pelo menos um dos seguintes: senha, certificado, chave simétrica, chave assimétrica ou provedor. A chave pode ter mais de uma criptografia de cada tipo. Em outras palavras, uma única chave simétrica pode ser criptografada com o uso de vários certificados, senhas, chaves simétricas e chaves assimétricas ao mesmo tempo.  
  
- Quando uma chave simétrica é criptografada com uma senha e não com a chave pública da chave mestre do banco de dados, o algoritmo de criptografia TRIPLE DES é usado. Por esse motivo, as chaves criadas com um algoritmo de criptografia forte, como AES, são protegidas por um algoritmo mais fraco.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY SYMMETRIC KEY no banco de dados. Se AUTHORIZATION for especificada, será necessária a permissão IMPERSONATE no usuário de banco de dados ou a permissão ALTER na função de aplicativo. Se a criptografia for por certificado ou chave assimétrica, exigirá a permissão VIEW DEFINITION no certificado ou na chave assimétrica. Somente logons do Windows, logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e funções de aplicativo podem ter chaves simétricas. Grupos e funções não podem possuir chaves simétricas.  
  
## <a name="using-transact-sql"></a>Usando Transact-SQL  
  
### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>Para criar chaves simétricas idênticas em dois servidores diferentes  
  
1. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2. Na barra Padrão, clique em **Nova Consulta**.  
  
3. Crie a chave executando as instruções CREATE MASTER KEY, CREATE CERTIFICATE e CREATE SYMMETRIC KEY.  
  
    ```sql
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
  
4. Conecte a uma instância de servidor separada, abra uma Janela de Consulta diferente e execute as instruções SQL acima para criar a mesma chave no segundo servidor.  
  
5. Teste as chaves executando primeiro a instrução OPEN e a instrução SELECT abaixo no primeiro servidor.  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6. No segundo servidor, cole o resultado da instrução SELECT anterior no seguinte código como o valor de `@blob` e execute esse código para verificar se a chave duplicada pode descriptografar o texto cifrado.  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7. Feche a chave simétrica em ambos os servidores.  
  
    ```sql
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  

### <a name="encryption-changes-in-sql-server-2017-cu2"></a>Alterações de criptografia no SQL Server 2017 CU2

O SQL Server 2016 usa o algoritmo de hash SHA1 em seu trabalho de criptografia. O SHA2 é usado desde o SQL Server 2017. Dessa maneira, talvez você precise de mais etapas para que a instalação do SQL Server 2017 descriptografe itens que eram criptografados pelo SQL Server 2016. Confira as etapas adicionais:

- Verifique se o SQL Server 2017 está atualizado ao menos para CU2 (Atualização Cumulativa 2).
  - Confira [CU2 (Atualização Cumulativa 2) para SQL Server 2017](https://support.microsoft.com/help/4052574) para ver detalhes importantes.
- Após a instalação da CU2, ative o sinalizador de rastreamento 4631 no SQL Server 2017: `DBCC TRACEON(4631, -1);`
  - O sinalizador de rastreamento 4631 é novo no SQL Server 2017. O sinalizador de rastreamento 4631 precisa estar `ON` globalmente antes da criação da chave mestra, do certificado ou da chave simétrica no SQL Server 2017. Dessa maneira, os itens criados poderão interoperar com o SQL Server 2016 e as versões anteriores.

Para ver mais diretrizes, confira:

- [CORREÇÃO: O SQL Server 2017 não pode descriptografar dados criptografados por versões anteriores do SQL Server usando a mesma chave simétrica](https://support.microsoft.com/help/4053407/sql-server-2017-cannot-decrypt-data-encrypted-by-earlier-versions)
- [Chaves simétricas idênticas não funcionam entre o SQL Server 2017 e outra versão do SQL Server](https://feedback.azure.com/forums/908035-sql-server/suggestions/33116269-identical-symmetric-keys-do-not-work-between-sql-s) <!-- Issue 2225. Thank you Stephen W and Sam Rueby. -->

## <a name="for-more-information"></a>Para obter mais informações

-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
