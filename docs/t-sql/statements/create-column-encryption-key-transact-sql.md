---
title: CREATE COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_COLUMN_ENCRYPTION_KEY_TSQL
- SQL13.SWB.NEWCOLUMNENCRYPTIONKEY.GENERAL.F1
- ENCRYPTION_KEY_TSQL
- CREATE COLUMN ENCRYPTION KEY
- ENCRYPTION KEY
- COLUMN ENCRYPTION KEY
- CREATE_COLUMN_ENCRYPTION_TSQL
- SQL13.SWB.COLUMNENCRYPTIONKEY.GENERAL.F1
- COLUMN_ENCRYPTION_KEY_TSQL
- CREATE COLUMN ENCRYPTION
dev_langs:
- TSQL
helpviewer_keywords:
- Always Encrypted, create column encryption key
- column encryption key, create
- column encryption key
- CREATE COLUMN ENCRYPTION KEY statement
ms.assetid: 517fe745-d79b-4aae-99a7-72be45ea6acb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3789e894f08c4e34cb5ea8861d699f850e365f3
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064568"
---
# <a name="create-column-encryption-key-transact-sql"></a>CREATE COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Cria uma chave de criptografia de coluna (CEK) com o conjunto inicial de valores, criptografadas com as chaves mestras de coluna (CMKs) especificadas. Esta criptografia é uma operação de metadados. Uma CEK pode ter até dois valores que permitem uma rotação de CMK. A criação de uma CEK é necessária antes que o recurso [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) criptografe qualquer coluna do banco de dados. Também é possível criar CEKs usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Antes de criar uma CEK, você deve definir uma CMK usando a instrução [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE COLUMN ENCRYPTION KEY key_name   
WITH VALUES  
  (  
    COLUMN_MASTER_KEY = column_master_key_name,   
    ALGORITHM = 'algorithm_name',   
    ENCRYPTED_VALUE = varbinary_literal  
  )   
[, (  
    COLUMN_MASTER_KEY = column_master_key_name,   
    ALGORITHM = 'algorithm_name',   
    ENCRYPTED_VALUE = varbinary_literal  
  ) ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
_key\_name_  
É o nome pelo qual a chave de criptografia da coluna será conhecida no banco de dados.  
  
_column\_master\_key\_name_ Especifica o nome da CMK personalizada usada para criptografar a CEK.  
  
_algorithm\_name_  
Nome do algoritmo de criptografia usado para criptografar o valor da chave de criptografia de coluna. O algoritmo para os provedores do sistema deve ser **RSA_OAEP**.  
  
_varbinary\_literal_  
O BLOB do valor CEK criptografado.  
  
> [!WARNING]  
>  Nunca passe valores de CEK de texto não criptografado nesta instrução. Fazer isso comprometerá o benefício desse recurso.  
  
## <a name="remarks"></a>Remarks  
A instrução CREATE COLUMN ENCRYPTION KEY deve incluir pelo menos uma cláusula VALUES e pode ter até duas. Se apenas uma for fornecida, você poderá usar a instrução ALTER COLUMN ENCRYPTION KEY para adicionar um segundo valor posteriormente. Você também pode usar a instrução ALTER COLUMN ENCRYPTION KEY para remover uma cláusula VALUES.  
  
Normalmente uma CEK é criada com apenas um valor criptografado. Às vezes, você precisa girar uma CMK. Substitua a CMK atual pela nova CMK. Quando for necessário girar a chave, adicione um novo valor de chave de criptografia de coluna, criptografado com a nova CMK. Essa rotação permite que você garanta que os aplicativos cliente possam acessar dados criptografados com a CEK, enquanto a nova CEK é disponibilizada para os aplicativos cliente. Um driver habilitado como Always Encrypted em um aplicativo cliente que não tem acesso à nova chave mestra usará o valor de CEK criptografado com a antiga CMK para acessar dados confidenciais.  
  
Os algoritmos de criptografia, compatíveis com o Always Encrypted, exigem que o valor de texto sem formatação tenha 256 bits.  
  
Um valor criptografado deve ser gerado com um provedor de repositório de chaves que encapsula o repositório de chaves que contém a CMK. Para obter mais informações, veja [Always Encrypted &#40;desenvolvimento de cliente&#41;](../../relational-databases/security/encryption/always-encrypted-client-development.md).  
  
Use [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md), e [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) para exibir informações sobre chaves de criptografia de coluna.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão **ALTER ANY COLUMN ENCRYPTION KEY**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-column-encryption-key"></a>A. Criando uma chave de criptografia de coluna  
O exemplo a seguir cria uma chave de criptografia de coluna chamada `MyCEK`.  
  
```sql  
CREATE COLUMN ENCRYPTION KEY MyCEK   
WITH VALUES  
(  
    COLUMN_MASTER_KEY = MyCMK,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x01700000016C006F00630061006C006D0061006300680069006E0065002F006D0079002F003200660061006600640038003100320031003400340034006500620031006100320065003000360039003300340038006100350064003400300032003300380065006600620063006300610031006300284FC4316518CF3328A6D9304F65DD2CE387B79D95D077B4156E9ED8683FC0E09FA848275C685373228762B02DF2522AFF6D661782607B4A2275F2F922A5324B392C9D498E4ECFC61B79F0553EE8FB2E5A8635C4DBC0224D5A7F1B136C182DCDE32A00451F1A7AC6B4492067FD0FAC7D3D6F4AB7FC0E86614455DBB2AB37013E0A5B8B5089B180CA36D8B06CDB15E95A7D06E25AACB645D42C85B0B7EA2962BD3080B9A7CDB805C6279FE7DD6941E7EA4C2139E0D4101D8D7891076E70D433A214E82D9030CF1F40C503103075DEEB3D64537D15D244F503C2750CF940B71967F51095BFA51A85D2F764C78704CAB6F015EA87753355367C5C9F66E465C0C66BADEDFDF76FB7E5C21A0D89A2FCCA8595471F8918B1387E055FA0B816E74201CD5C50129D29C015895CD073925B6EA87CAF4A4FAF018C06A3856F5DFB724F42807543F777D82B809232B465D983E6F19DFB572BEA7B61C50154605452A891190FB5A0C4E464862CF5EFAD5E7D91F7D65AA1A78F688E69A1EB098AB42E95C674E234173CD7E0925541AD5AE7CED9A3D12FDFE6EB8EA4F8AAD2629D4F5A18BA3DDCC9CF7F352A892D4BEBDC4A1303F9C683DACD51A237E34B045EBE579A381E26B40DCFBF49EFFA6F65D17F37C6DBA54AA99A65D5573D4EB5BA038E024910A4D36B79A1D4E3C70349DADFF08FD8B4DEE77FDB57F01CB276ED5E676F1EC973154F86  
);  
GO  
```  
  
### <a name="creating-a-column-encryption-key-with-two-values"></a>Criar uma Chave de Criptografia de Coluna com dois valores  
O exemplo a seguir cria uma chave de criptografia de coluna chamada `TwoValueCEK` com dois valores.  
  
```sql

CREATE COLUMN ENCRYPTION KEY TwoValueCEK   
WITH VALUES  
(  
    COLUMN_MASTER_KEY = CMK1,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0037006300380061003100310033003400320037003800620037003000630038003100390062003900630039003400360061006600340039006500610030003200650038006200650038003400340065006C33A82ECF04A7185824B4545457AC5244CD9C219E64067B9520C0081B8399B58C2863F7494ABE3694BD87D55FFD7576FFDC47C28F94ECC99577DF4FB8FA19AA95764FEF889CDE0F176DA5897B74382FBB22756CE2921050A09201A0EB6AF3D6091014C30146EA62635EE8CBF0A8074DEDFF125CEA80D1C0F5E8C58750A07D270E2A8BF824EE4C0C156366BF26D38CCE49EBDD5639A2DF029A7DBAE5A5D111F2F2FA3246DF8C2FA83C1E542C10570FADA98F6B29478DC58CE5CBDD407CCEFCDB97814525F6F32BECA266014AC346AC39C4F185C6C0F0A24FEC4DFA015649624692DE7865B9827BA22C3B574C9FD169F822B609F902288C5880EB25F14BD990D871B1BC4BA3A5B237AF76D26354773FA2A25CF4511AF58C911E601CFCB1905128C997844EED056C2AE7F0B48700AB41307E470FF9520997D0EB0D887DE11AFE574FFE845B7DC6C03FEEE8D467236368FC0CB2FDBD54DADC65B10B3DE6C80DF8B7B3F8F3CE5BE914713EE7B1FA5B7A578359592B8A5FDFDDE5FF9F392BC87C3CD02FBA94582AC063BBB9FFAC803FD489E16BEB28C4E3374A8478C737236A0B232F5A9DDE4D119573F1AEAE94B2192B81575AD6F57E670C1B2AB91045124DFDAEC2898F3F0112026DFC93BF9391D667D1AD7ED7D4E6BB119BBCEF1D1ADA589DD3E1082C3DAD13223BE438EB9574DA04E9D8A06320CAC6D3EC21D5D1C2A0AA484C7C  
),  
(  
    COLUMN_MASTER_KEY = CMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
[DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
[CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
[Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
[sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
[sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
