---
description: ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
title: ALTER COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: a90e0e787abdaedb4cde1a3461349fcd521c6cf9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646386"
---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Altera uma chave de criptografia de coluna em um banco de dados, adicionando ou removendo um valor criptografado. Uma chave de criptografia de chave pode ter até dois valores, o que permite a rotação da chave mestra de coluna correspondente. Uma chave de criptografia de coluna é usada ao criptografar colunas usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) ou [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md). Antes de adicionar um valor de chave de criptografia de coluna, é necessário definir a chave mestra de coluna que foi usada para criptografar o valor usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou a instrução [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  

## <a name="arguments"></a>Argumentos
 *key_name*  
 A chave de criptografia de coluna que está sendo alterada.  
  
 *column_master_key_name*  
 Especifica o nome da CMK (chave mestra de coluna) usada para criptografar a CEK (chave de criptografia de coluna).  
  
 *algorithm_name*  
 Nome do algoritmo de criptografia usado para criptografar o valor. O algoritmo para os provedores do sistema deve ser **RSA_OAEP**. Esse argumento não é válido durante a remoção de um valor de chave de criptografia de coluna.  
  
 *varbinary_literal*  
 O BLOB de CEK criptografado com a chave mestra de criptografia especificada. Esse argumento não é válido durante a remoção de um valor de chave de criptografia de coluna.  
  
> [!WARNING]  
>  Nunca passe valores de CEK de texto não criptografado nesta instrução. Fazer isso comprometerá o benefício desse recurso.  

## <a name="remarks"></a>Comentários
Normalmente, uma chave de criptografia de coluna é criada com apenas um valor criptografado. Quando uma chave mestra de coluna precisar ser girada (a chave mestra de coluna atual precisa ser substituída pela nova chave mestra de coluna), adicione um novo valor da chave de criptografia de coluna, criptografado com a nova chave mestra de coluna. Esse fluxo de trabalho permitirá que você garanta que os aplicativos cliente possam acessar dados criptografados com a chave de criptografia de coluna enquanto a nova chave mestra de coluna está sendo disponibilizada para os aplicativos cliente. Um driver habilitado para Always Encrypted em um aplicativo cliente que não tem acesso à nova chave mestra poderá usar o valor de chave de criptografia de coluna criptografado com a chave mestra de coluna antiga para acessar dados confidenciais. Os algoritmos de criptografia, compatíveis com o Always Encrypted, exigem que o valor de texto sem formatação tenha 256 bits. 
 
É recomendável usar ferramentas, como o SSMS (SQL Server Management Studio) ou o PowerShell para alternar chaves mestras de coluna. Confira [Alternar chaves do Always Encrypted usando o SQL Server Management Studio](../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-ssms.md) e [Alternar chaves do Always Encrypted usando o PowerShell](../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md).

Um valor criptografado deve ser gerado com um provedor de repositório de chaves que encapsula o repositório de chaves que contém a chave mestra de coluna.  

 As chaves mestras de coluna são giradas pelos seguintes motivos:
- Normas de conformidade podem exigir que as chaves sejam giradas periodicamente.
- Uma chave mestra de coluna está comprometida e precisa ser girada por motivos de segurança.
- Para habilitar ou desabilitar o compartilhamento de chaves de criptografia de coluna com um enclave seguro no lado do servidor. Por exemplo, se sua chave mestra de coluna atual não dá suporte a cálculos de enclave (não foi definida com a propriedade ENCLAVE_COMPUTATIONS) e você deseja habilitar cálculos de enclave em colunas protegidas com uma chave de criptografia coluna que sua chave mestra de coluna criptografa, você precisa substituir a chave mestra de coluna pela nova chave com a propriedade ENCLAVE_COMPUTATIONS. [Visão geral do gerenciamento de chaves do Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) e [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md).

Use [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) e [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) para exibir informações sobre chaves de criptografia de coluna.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **ALTER ANY COLUMN ENCRYPTION KEY** no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-column-encryption-key-value"></a>a. Adicionando um valor de chave de criptografia de coluna  
 O exemplo a seguir altera uma chave de criptografia de coluna chamada `MyCEK`.  
  
```sql  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. Removendo um valor de chave de criptografia de coluna  
 O exemplo a seguir altera uma chave de criptografia de coluna chamada `MyCEK` removendo um valor.  
  
```sql  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Visão geral do gerenciamento de chaves do Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Gerenciar chaves para Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
  
