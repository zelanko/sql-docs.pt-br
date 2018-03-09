---
title: sp_refresh_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
caps.latest.revision: "3"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9343880058cef4ef86ce16613bc43821e8e8a24
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="sprefreshparameterencryption-transact-sql"></a>sp_refresh_parameter_encryption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Atualiza os metadados sempre criptografado para os parâmetros do procedimento armazenado de não associadas a esquema especificado, função definida pelo usuário, exibição, DML disparador, gatilho DDL de nível de banco de dados ou gatilho DDL de nível de servidor no banco de dados atual. 

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>Argumentos

[  **@name =** ] **'***nome_de_módulo***'**   
É o nome do procedimento armazenado, função definida pelo usuário, exibição, gatilho DML, gatilho DDL de nível do banco de dados ou gatilho DDL do nível de servidor. *nome_de_módulo* não pode ser um tempo de execução de linguagem comum (CLR) procedimento armazenado ou uma função CLR. *nome_de_módulo* não pode ser associada a esquema. *nome_de_módulo* é `nvarchar`, sem padrão. *nome_de_módulo* pode ser um identificador de várias partes, mas só pode fazer referência a objetos no banco de dados atual.

[  **@namespace =** ] **'** < classe > **'**   
É a classe do módulo especificado. Quando *nome_de_módulo* é um gatilho DDL, `<class>` é necessária. `<class>`is `nvarchar(20)`. As entradas válidas são `DATABASE_DDL_TRIGGER` e `SERVER_DDL_TRIGGER`.    

## <a name="return-code-values"></a>Valores do código de retorno  

0 (êxito) ou um número diferente de zero (falha)


## <a name="remarks"></a>Remarks

Os metadados de criptografia para os parâmetros de um módulo podem se tornar desatualizados, se:   
* Propriedades de criptografia de uma coluna em uma tabela de referências de módulo, foram atualizados. Por exemplo, uma coluna foi removida e uma nova coluna com o mesmo nome, mas um tipo de criptografia diferente, chave de criptografia ou um algoritmo de criptografia foi adicionada.  
* O módulo faz referência a outro módulo com metadados de criptografia do parâmetro desatualizado.  

Quando as propriedades de criptografia de uma tabela são modificadas, `sp_refresh_parameter_encryption` deve ser executado para quaisquer módulos direta ou indiretamente faz referência à tabela. Esse procedimento armazenado pode ser chamado nesses módulos em qualquer ordem, sem exigir que o usuário para o módulo interno de primeira atualização antes de passar para chamadores.

`sp_refresh_parameter_encryption`não afeta nenhuma permissão, propriedades estendidas, ou `SET` opções que estão associadas ao objeto. 

Para atualizar um gatilho DDL de nível de servidor, execute este procedimento armazenado a partir do contexto de qualquer banco de dados.

>  [!NOTE]   
>  Assinaturas que estão associadas ao objeto são removidas quando você executar `sp_refresh_parameter_encryption`.

## <a name="permissions"></a>Permissões

Requer `ALTER` permissão no módulo e `REFERENCES` permissão em qualquer tipos CLR definidos pelo usuário e coleções de esquema XML que são referenciadas pelo objeto.   

Quando o módulo especificado for um gatilho DDL de nível de banco de dados, requer `ALTER ANY DATABASE DDL TRIGGER` no banco de dados atual.    

Quando o módulo especificado for um gatilho DDL de nível de servidor, requer `CONTROL SERVER` permissão.

Para os módulos que são definidos com o `EXECUTE AS` cláusula `IMPERSONATE` permissão é necessária no principal especificado. Em geral, a atualização de um objeto não altera seu `EXECUTE AS` principal, a menos que o módulo foi definido com `EXECUTE AS USER` e o nome de usuário da entidade de segurança agora resolve para um usuário diferente do que no momento em que o módulo foi criado.
 
## <a name="examples"></a>Exemplos

O exemplo a seguir cria uma tabela e um procedimento que fazem referência à tabela, configura o sempre criptografado e, em seguida, demonstra alterando a tabela e em execução o `sp_refresh_parameter_encryption` procedimento.  

Primeiro, crie a tabela inicial e um procedimento armazenado que faz referência à tabela.
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

Configure as chaves do sempre criptografado.
```sql
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
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


Por fim, substituímos a coluna SSN com a coluna criptografada e, em seguida, executa o `sp_refresh_parameter_encryption` procedimento para atualizar os componentes de sempre criptografado.
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>Consulte Também 

[Sempre criptografado](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Assistente do Always Encrypted](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

