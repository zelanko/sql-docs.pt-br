---
title: sp_describe_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_parameter_encryption
- sp_describe_parameter_encryption_TSQL
- sys.sp_describe_parameter_encryption
- sys.sp_describe_parameter_encryption_TSQL
helpviewer_keywords:
- sp_describe_parameter_encryption
ms.assetid: 706ed441-2881-4934-8d5e-fb357ee067ce
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 243207c6175f5604e7cc887bd7c67085e2d86291
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507638"
---
# <a name="spdescribeparameterencryption-transact-sql"></a>sp_describe_parameter_encryption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Analisa especificado [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução e seus parâmetros, para determinar quais parâmetros correspondem às colunas de banco de dados que são protegidas usando o recurso Always Encrypted. Retorna os metadados de criptografia para os parâmetros que correspondem a colunas criptografadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ \@tsql =] 'Transact-SQL_batch'  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. SQL_batch Transact pode ser nvarchar (n) ou nvarchar (max).  
  
 [ \@params =] 'N'parameters  
 *\@params* fornece uma cadeia de caracteres de declaração para os parâmetros para o lote Transact-SQL, que é similar a sp_executesql. Parâmetros podem ser nvarchar (n) ou nvarchar (max).  
  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos no [!INCLUDE[tsql](../../includes/tsql-md.md)]_batch. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetro adicionais. Todo parâmetro especificado na instrução deve ser definido em  *\@params*. Se o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote na instrução não contiverem parâmetros,  *\@params* não é necessária. NULL é o valor padrão para esse parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 0 indica êxito. Qualquer outra coisa indicam falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_describe_parameter_encryption** retorna dois conjuntos de resultados:  
  
-   O conjunto de resultados que descreve as chaves criptográficas configuradas para colunas de banco de dados, os parâmetros de especificado [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução correspondem às.  
  
-   Descrever específico como parâmetros de conjunto de resultados devem ser criptografados. Este conjunto de resultados referências as chaves descritas no primeiro conjunto de resultados.  
  
 Cada linha do primeiro conjunto de resultados descreve um par de chaves; uma chave de criptografia de coluna criptografada e sua chave mestra de coluna correspondente.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|ID da linha no conjunto de resultados.|  
|**database_id**|**int**|Id do banco de dados.|  
|**column_encryption_key_id**|**int**|A id de chave de criptografia de coluna. Observação: essa id denota uma linha na [column_encryption_keys &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) exibição de catálogo.|  
|**column_encryption_key_version**|**int**|Reservado para uso futuro. Atualmente, contém sempre 1.|  
|**column_encryption_key_metadata_version**|**binary(8)**|Um carimbo de hora que representa a hora de criação da chave de criptografia de coluna.|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|O valor criptografado da chave de criptografia de coluna.|  
|**column_master_key_store_provider_name**|**sysname**|O nome do provedor de repositório de chaves que contém a chave mestra de coluna que foi usada para produzir o valor criptografado da chave de criptografia de coluna.|  
|**column_master_key_path**|**nvarchar(4000)**|O caminho da chave da chave mestra de coluna, o que foi usada para produzir o valor criptografado da chave de criptografia de coluna.|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|O nome do algoritmo de criptografia usado para gerar o valor de criptografia da chave de criptografia de coluna.|  
  
 Cada linha do segundo conjunto de resultados contém metadados de criptografia para um parâmetro.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|ID da linha no conjunto de resultados.|  
|**parameter_name**|**sysname**|Nome de um dos parâmetros especificados na  *\@params* argumento.|  
|**column_encryption_algorithm**|**tinyint**|Código que indica o algoritmo de criptografia configurado para a coluna, o parâmetro corresponde à. Os valores com suporte no momento são: 2 para **AEAD_AES_256_CBC_HMAC_SHA_256**.|  
|**column_encryption_type**|**tinyint**|Código que indica o tipo de criptografia configurado para a coluna, o parâmetro corresponde à. Os valores com suporte são:<br /><br /> 0 - texto sem formatação (a coluna não é criptografada)<br /><br /> 1 - a criptografia aleatória<br /><br /> 2 - a criptografia determinística.|  
|**column_encryption_key_ordinal**|**int**|O código da linha em que o primeiro resultado definido. A linha referenciada descreve a chave de criptografia de coluna configurada para a coluna, o parâmetro corresponde à.|  
|**column_encryption_normalization_rule_version**|**tinyint**|Número de versão do algoritmo de normalização de tipo.|  
  
## <a name="remarks"></a>Comentários  
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver do cliente, que dão suporte a Always Encrypted, chama automaticamente **sp_describe_parameter_encryption** para recuperar metadados de criptografia para consultas parametrizadas, emitida pelo aplicativo. Subsequentemente, o driver usa os metadados de criptografia para criptografar os valores de parâmetros que correspondem às colunas de banco de dados protegidas com o Always Encrypted e substitui os valores de parâmetro de texto sem formatação, enviados pelo aplicativo, com o criptografado valores de parâmetro, antes de enviar a consulta para o mecanismo de banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Exigir a **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** e **VIEW ANY COLUMN MASTER KEY DEFINITION** permissões no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
```  
CREATE COLUMN MASTER KEY [CMK1]  
WITH  
(  
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',  
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'  
);  
GO  
  
CREATE COLUMN ENCRYPTION KEY [CEK1]  
WITH VALUES  
(  
       COLUMN_MASTER_KEY = [CMK1],  
    ALGORITHM = 'RSA_OAEP',  
    ENCRYPTED_VALUE =   
0x016E000001630075007200720065006E00740075007300650072002F006D007  
9002F00610036003600620062003000660036006400640037003000620064006  
6006600300032006200360032006400300066003800370065003300340030003  
200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF991  
37B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA51  
7A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6  
686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015B  
DB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8  
C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE3  
74DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A3472  
3276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550E  
C5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E0  
35175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D8  
01ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B  
4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF8  
1A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202F  
C24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B0195883360  
4707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E  
9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C  
3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085  
);  
GO  
  
CREATE TABLE t1 (  
c1 INT ENCRYPTED WITH (  
    COLUMN_ENCRYPTION_KEY = [CEK_Auto1],   
    ENCRYPTION_TYPE = Randomized,   
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL,  
);  
  
EXEC sp_describe_parameter_encryption N'INSERT INTO t1 VALUES(@c1)',  N'@c1 INT';  
```  
  
 Aqui está o primeiro conjunto de resultados:  
  
|column_encryption_key_ordinal|database_id|column_encryption_key_id|column_encryption_key_version|column_encryption_key_metadata_version|column_encryption_key_encrypted_value|  
|--------------------------------------|------------------|---------------------------------|--------------------------------------|------------------------------------------------|-----------------------------------------------|  
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA 74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232 F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE2439 2D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B3864 87CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 (Continuam resultados).  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 Aqui está o segundo conjunto de resultados:  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@C1|1|1|  
  
 (Continuam resultados).  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>Consulte também  
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted &#40;desenvolvimento de cliente&#41;](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
