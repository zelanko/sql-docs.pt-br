---
title: Índices em colunas habilitadas para enclave com criptografia aleatória (tutorial)
description: Este tutorial ensina a criar e usar índices em colunas habilitadas para enclave usando a criptografia aleatória com suporte no Always Encrypted com enclaves seguros no SQL Server.
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9ddfb9836650028c0f6aae150a2f70e4758b6ca2
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279272"
---
# <a name="tutorial-create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Tutorial: Criar e usar índices em colunas habilitadas para enclave com criptografia aleatória
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Este tutorial ensina como criar e usar índices em colunas habilitadas para enclave usando a criptografia aleatória com suporte em [Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves.md). Ela mostrará a você:

- Como criar um índice quando você tem acesso às chaves (à chave mestra de coluna e à chave de criptografia de coluna) que protegem a coluna.
- Como criar um índice quando você não tem acesso às chaves de proteção da coluna.

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial é a continuação do [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](./tutorial-getting-started-with-always-encrypted-enclaves.md). Você precisa concluí-lo antes de prosseguir para as próximas etapas.

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>Etapa 1: Habilitar ADR (Recuperação de Banco de Dados Acelerada) no banco de dados

A Microsoft recomenda habilitar a ADR em seu banco de dados antes de criar o primeiro índice em uma coluna habilitada para enclave usando a criptografia aleatória. Confira a seção [Recuperação de banco de dados](./encryption/always-encrypted-enclaves.md#database-recovery) em [Always Encrypted com enclaves seguros](./encryption/always-encrypted-enclaves.md).

1. Feche todas as instâncias SSMS usadas no tutorial anterior. Isso fechará as conexões de banco de dados que você abriu, o que é necessário para habilitar a ADR.
1. Abra uma nova instância do SSMS e conecte-se à instância do SQL Server como sysadmin **sem** Always Encrypted habilitado para a conexão de banco de dados.
    1. Inicie o SSMS.
    1. Na caixa de diálogo **Conectar ao servidor**, especifique o nome do servidor, selecione um método de autenticação e especifique suas credenciais.
    1. Clique em **Opções >>** e selecione a guia **Always Encrypted**.
    1. Verifique se a caixa de seleção **Habilitar o Always Encrypted (criptografia de coluna)** **não** está selecionada.
    1. Selecione **Conectar**.
1. Abra uma nova janela de consulta e execute a instrução abaixo para habilitar a ADR.

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>Etapa 2: Criar e testar um índice sem separação de funções

Nesta etapa, você criará e testará um índice em uma coluna criptografada. Você atuará como um único usuário que assume as funções de DBA, que gerencia o banco de dados e é o proprietário dos dados com acesso às chaves de proteção de dados.

1. Abra uma nova instância do SSMS e conecte-se à instância do SQL Server **com** Always Encrypted habilitado para a conexão de banco de dados.
   1. Inicie uma nova instância do SSMS.
   1. Na caixa de diálogo **Conectar ao servidor**, especifique o nome do servidor, selecione um método de autenticação e especifique suas credenciais.
   1. Clique em **Opções >>** e selecione a guia **Always Encrypted**.
   1. Marque a caixa de seleção **Habilitar o Always Encrypted (criptografia de coluna)** e especifique a URL do atestado do enclave (por exemplo, ht<span>tp://<   span>hgs.bastion.local/Attestation).
   1. Selecione **Conectar**.
   1. Se solicitado a habilitar a parametrização para consultas Always Encrypted, clique em **Habilitar**.
1. Se você não receber a solicitação para habilitar Parametrização para consultas Always Encrypted, verifique se a opção está habilitada.
   1. Selecione **Ferramentas** no menu principal do SSMS.
   2. Selecione **Opções...** .
   3. Navegue para **Execução da Consulta** > **SQL Server** > **Avançado**.
   4. A opção **Habilitar Parametrização do Always Encrypted** precisa estar marcada.
   5. Selecione **OK**.
1. Abra uma janela de consulta e execute as instruções abaixo para criptografar a coluna **LastName** na tabela **Funcionários**. Você criará e usará um índice nessa coluna em etapas posteriores.

   ```sql
   USE [ContosoHR];
   GO   
   ALTER TABLE [dbo].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. Crie um índice na coluna **LastName**. Uma vez que você esteja conectado ao banco de dados com o Always Encrypted habilitado, o driver do cliente dentro do SSMS fornecerá para o enclave, de forma transparente, a **CEK1** (a chave de criptografia de coluna que protege a coluna **LastName**), que é necessária para criar o índice.

   ```sql
   USE [ContosoHR];
   GO

   CREATE INDEX IX_LastName ON [Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. Execute uma consulta avançada na coluna **LastName** e verifique se o SQL Server usa o índice ao executar a consulta.
   1. Na mesma janela de consulta ou em uma nova, verifique se o botão **Incluir estatísticas de consulta ao vivo** da barra de ferramentas está ativado.
   1. Execute a consulta abaixo.

       ```sql
       USE [ContosoHR];
       GO

       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. Na guia **Estatísticas de consulta dinâmica** (na parte inferior da janela de consulta), observe se a consulta usa o índice.

## <a name="step-3-create-an-index-with-role-separation"></a>Etapa 3: Criar um índice com separação de funções

Nesta etapa, você criará um índice em uma coluna criptografada, fingindo ser dois usuários diferentes. Um usuário é um DBA que precisa para criar um índice, mas não tem acesso às chaves. O outro usuário é um proprietário de dados com acesso às chaves.

1. Usando a instância do SSMS **sem** Always Encrypted habilitado, execute a instrução abaixo para descartar o índice na coluna **LastName**.

   ```sql
   USE [ContosoHR];
   GO

   DROP INDEX IX_LastName ON [Employees]; 
   GO
   ```

1. Atuando como um proprietário de dados (ou um aplicativo que tenha acesso às chaves), popule o cache dentro de enclave com **CEK1**.

   > [!NOTE]
   > A menos que você tenha reiniciado a instância do SQL Server depois da **Etapa 2: Criar e testar um índice sem separação de funções**, essa etapa é redundante, pois o **CEK1** já está presente no cache. Ela foi adicionada para demonstrar como um proprietário de dados pode fornecer uma chave para o enclave, se ainda não estiver presente no enclave.

   1. Na instância de SSMS **com** o Always Encrypted habilitado, execute as instruções abaixo em uma janela de consulta. A instrução envia ao enclave todas as chaves de criptografia da coluna habilitada para o enclave. Confira [sp_enclave_send_keys](../system-stored-procedures/sp-enclave-send-keys-sql.md) para obter os detalhes.

        ```sql
        USE [ContosoHR];
        GO

        EXEC sp_enclave_send_keys;
        GO
        ```

   1. Como alternativa para executar o procedimento armazenado acima, você pode executar uma consulta DML que usa o enclave em comparação com a coluna **LastName**. Isso preencherá o enclave somente com **CEK1**.

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. Agindo como um DBA, crie o índice.
    1. Na instância de SSMS **sem** o Always Encrypted habilitado, execute as instruções abaixo em uma janela de consulta.

        ```sql
        USE [ContosoHR];
        GO

        CREATE INDEX IX_LastName ON [Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. Como proprietário de dados, execute uma consulta avançada na coluna **LastName** e verifique se o SQL Server usa o índice ao executar a consulta.
   1. Na instância do SSMS **com** Always Encrypted habilitado, selecione uma janela de consulta existente ou abra uma nova janela de consulta e verifique se o botão **Incluir estatísticas de consulta ao vivo** está habilitado na barra de ferramentas.
   1. Execute a consulta abaixo. 

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. Na guia **Estatísticas de consulta dinâmica** (na parte inferior da janela de consulta), observe se a consulta usa o índice.

## <a name="next-steps"></a>Próximas etapas
- [Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>Confira também
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves-create-use-indexes.md)
