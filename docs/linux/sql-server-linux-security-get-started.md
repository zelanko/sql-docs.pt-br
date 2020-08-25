---
title: Introdução à segurança do SQL Server em Linux
description: Percorra os recursos de segurança do SQL Server em Linux para ter uma ideia das áreas a serem investigadas.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 031005dcb6a5353e9e4f0b73a7a45d667d2212e7
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088788"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Passo a passo dos recursos de segurança do SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Se você for um usuário do Linux não familiarizado com o SQL Server, as tarefas a seguir o orientarão em algumas das tarefas de segurança. Elas não são exclusivas nem específicas do Linux, mas ajudam a dar uma ideia de áreas para posterior investigação. Em cada exemplo, um link é fornecido para a documentação detalhada dessa área.

> [!NOTE]
>  Os exemplos a seguir usam o banco de dados de exemplo **AdventureWorks2014**. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, confira [Restaurar um banco de dados do SQL Server do Windows para o Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Criar um logon e um usuário de banco de dados 

Permite a outros usuários o acesso ao SQL Server criando um logon no banco de dados mestre usando a instrução [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md). Por exemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Sempre use uma senha forte no lugar dos asteriscos no comando anterior.

Os logons podem se conectar ao SQL Server e ter acesso (com permissões limitadas) ao banco de dados mestre. Para se conectar a um banco de dados de usuário, um logon precisa ter uma identidade correspondente no nível de banco de dados, chamada usuário de banco de dados. Os usuários são específicos de cada banco de dados e precisam ser criados separadamente em cada banco de dados para permitir acesso a eles. O exemplo a seguir insere você no banco de dados AdventureWorks2014 e, em seguida, usa a instrução [CREATE USER](../t-sql/statements/create-user-transact-sql.md) para criar um usuário chamado Paulo que está associado ao logon chamado Paulo. Embora o logon e o usuário estejam relacionados (mapeados entre si), eles são objetos diferentes. O logon é uma entidade de segurança no nível do servidor. O usuário é uma entidade de segurança no nível do banco de dados.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Uma conta de administrador do SQL Server pode se conectar a qualquer banco de dados e pode criar mais logons e usuários em qualquer banco de dados.  
- Quando alguém cria um banco de dados, ele se torna o proprietário do banco de dados, que pode se conectar a esse banco de dados. Os proprietários do banco de dados podem criar mais usuários.

Posteriormente, você pode autorizar outros logons a criar mais logons, concedendo a eles a permissão `ALTER ANY LOGIN`. Em um banco de dados, você pode autorizar outros usuários a criarem mais usuários concedendo a eles a permissão `ALTER ANY USER`. Por exemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Agora o logon Paulo pode criar mais logons e o usuário Marco pode criar mais usuários.


## <a name="granting-access-with-least-privileges"></a>Como permitir acesso com privilégios mínimos

As primeiras pessoas a se conectarem a um banco de dados de usuário serão as contas de administrador e proprietário do banco de dados. No entanto, esses usuários têm todas as permissões disponíveis no banco de dados. Isso representa um número de permissões além do que a maioria dos usuários deve ter. 

Quando você estiver apenas começando, poderá atribuir algumas categorias gerais de permissões usando as *funções de banco de dados fixas* internas. Por exemplo, a função de banco de dados fixa `db_datareader` pode ler todas as tabelas no banco de dados, mas não pode fazer nenhuma alteração. Permita a associação em uma função de banco de dados fixa usando a instrução [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md). O exemplo a seguir adiciona o usuário `Jerry` à função de banco de dados fixa `db_datareader`.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obter uma lista das funções de banco de dados fixas, confira [Funções no nível do banco de dados](../relational-databases/security/authentication-access/database-level-roles.md).

Posteriormente, quando estiver pronto para configurar o acesso mais preciso aos seus dados (altamente recomendado), crie suas próprias funções de banco de dados definidas pelo usuário usando a instrução [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md). Em seguida, atribua permissões granulares específicas às funções personalizadas.

Por exemplo, as instruções a seguir criam uma função de banco de dados chamada `Sales`, concede ao grupo `Sales` a capacidade de ver, atualizar e excluir linhas da tabela `Orders` e, em seguida, adiciona o usuário `Jerry` à função `Sales`.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```

Para obter mais informações sobre o sistema de permissões, confira [Introdução às Permissões do Mecanismo de Banco de Dados](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## <a name="configure-row-level-security"></a>Configurar segurança em nível de linha  

A [Segurança em Nível de Linha](../relational-databases/security/row-level-security.md) permite restringir o acesso a linhas em um banco de dados com base no usuário que está executando uma consulta. Esse recurso é útil para cenários como a garantia de que os clientes possam acessar somente os próprios dados ou que os trabalhadores possam acessar apenas os dados pertinentes ao departamento deles.   

As etapas a seguir explicam como configurar dois usuários com acesso de nível de linha diferente à tabela `Sales.SalesOrderHeader`. 

Crie duas contas de usuário para testar a segurança em nível de linha:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```

Conceda acesso de leitura à tabela `Sales.SalesOrderHeader` para ambos os usuários:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;
```
   
Crie um esquema e uma função com valor de tabela embutida. A função retorna 1 quando uma linha na coluna `SalesPersonID` corresponde à ID de um logon `SalesPerson` ou se o usuário que executa a consulta é o usuário Gerente.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```

Crie uma política de segurança que adicione a função como um predicado de bloqueio e de filtro na tabela:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute o disposto a seguir para consultar a tabela `SalesOrderHeader` como cada usuário. Verifique se `SalesPerson280` vê apenas as 95 linhas das próprias vendas e se o `Manager` pode ver todas as linhas na tabela.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Altere a política de segurança para desabilitar a política específica.  Agora ambos os usuários podem acessar todas as linhas. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>Habilitar Máscara Dinâmica de Dados

A [Máscara Dinâmica de Dados](../relational-databases/security/dynamic-data-masking.md) permite limitar a exposição de dados confidenciais a usuários de um aplicativo por meio do mascaramento completo ou parcial de determinadas colunas. 

Use uma instrução `ALTER TABLE` para adicionar uma função de mascaramento à coluna `EmailAddress` na tabela `Person.EmailAddress`: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Crie um usuário `TestUser` com a permissão `SELECT` na tabela e execute uma consulta como `TestUser` para ver os dados mascarados:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verifique se a função de mascaramento altera o endereço de email no primeiro registro de:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>Habilitar Transparent Data Encryption

Uma ameaça ao seu banco de dados é o risco de que alguém roube os arquivos de banco de dados de sua unidade de disco rígido. Isso pode acontecer com uma intrusão que obtém acesso elevado ao seu sistema, por meio de ações de um funcionário problemático ou por roubo do computador que contém os arquivos (como um laptop).

A TDE (Transparent Data Encryption) criptografa os arquivos de dados conforme eles são armazenados no disco rígido. O banco de dados mestre do mecanismo de banco de dados do SQL Server tem a chave de criptografia para que o mecanismo de banco de dados possa manipular os dados. Os arquivos de banco de dados não podem ser lidos sem acesso à chave. Os administradores de alto nível podem gerenciar, fazer backup e recriar a chave, para que o banco de dados possa ser movido, mas apenas por pessoas selecionadas. Quando a TDE é configurada, o banco de dados `tempdb` também é criptografado automaticamente. 

Como o Mecanismo de Banco de Dados pode ler os dados, a Transparent Data Encryption não protege contra acesso não autorizado por administradores do computador que pode ler diretamente a memória ou acessar o SQL Server por meio de uma conta de administrador.

### <a name="configure-tde"></a>Configurar a TDE

- Crie uma chave mestra
- Crie ou obtenha um certificado protegido pela chave mestra
- Crie uma chave de criptografia de banco de dados e proteja-a com o certificado
- Defina o banco de dados para usar criptografia

Configurar a TDE requer a permissão `CONTROL` no banco de dados mestre e a permissão `CONTROL` no banco de dados do usuário. Normalmente, um administrador configura a TDE. 

O exemplo a seguir ilustra criptografia e descriptografia do banco de dados `AdventureWorks2014` usando um certificado instalado no servidor nomeado `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

Para remover a TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

As operações de criptografia e descriptografia são agendadas em threads em segundo plano pelo SQL Server. É possível exibir o status dessas operações usando exibições do catálogo e de gerenciamento dinâmico na lista mostrada posteriormente neste tópico.   

> [!WARNING]
>  Os arquivos de backup de bancos de dados com TDE habilitada também são criptografados usando a chave de criptografia do banco de dados. Como resultado, quando você restaura esses backups, o certificado que protege a chave de criptografia do banco de dados deve estar disponível. Isso significa que, além de fazer backup do banco de dados, você deve assegurar que os backups dos certificados de servidor sejam mantidos para evitar perda de dados. Se o certificado não estiver mais disponível, haverá perda de dados. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

Para obter mais informações sobre a TDE, confira [TDE (Transparent Data Encryption)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## <a name="configure-backup-encryption"></a>Configurar a criptografia de backup
O SQL Server tem a capacidade de criptografar os dados durante a criação de um backup. Especificando o algoritmo de criptografia e o criptografador (um certificado ou uma chave assimétrica) ao criar um backup, você pode criar um arquivo de backup criptografado.    
  
> [!WARNING]
> É muito importante fazer backup do certificado ou da chave assimétrica e, preferencialmente, em um local diferente do arquivo de backup usado para criptografar. Sem o certificado ou a chave assimétrica, você não pode restaurar o backup, tornando o arquivo de backup inutilizável. 
 
 
O exemplo a seguir cria um certificado e cria um backup protegido pelo certificado.

```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

Para obter mais informações, veja [Criptografia de backup](../relational-databases/backup-restore/backup-encryption.md).


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os recursos de segurança no SQL Server, confira [Central de Segurança para o Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
