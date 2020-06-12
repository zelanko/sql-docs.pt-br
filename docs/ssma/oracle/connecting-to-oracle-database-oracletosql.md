---
title: Conectando-se ao Oracle Database (OracleToSQL) | Microsoft Docs
description: Saiba como se conectar ao banco de dados Oracle para migrar esse banco de dados Oracle para SQL Server. O SSMA Obtém e exibe metadados sobre todos os esquemas Oracle.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 06/04/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
ms.author: alexiva
ms.openlocfilehash: d6fc63d62e9761f167eb70165c6f9324f56253a8
ms.sourcegitcommit: 38639b67a135ca1a50a8e38fa61a089efe90e3f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454529"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Conectar-se a um banco de dados Oracle (OracleToSQL)

Para migrar os bancos de dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar ao Oracle Database que deseja migrar. Quando você se conecta, o SSMA obtém metadados sobre todos os esquemas Oracle e, em seguida, exibe-os no painel do Gerenciador de metadados Oracle. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena senhas.

A conexão com o banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados.

Os metadados sobre o banco de dados Oracle não são atualizados automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados Oracle, deverá atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualizando metadados do Oracle" mais adiante neste tópico.

## <a name="required-oracle-permissions"></a>Permissões do Oracle necessárias

No mínimo, a conta usada para se conectar ao banco de dados Oracle deve ter as seguintes permissões:

- `CONNECT`  
  Necessário para conectar-se (criar uma sessão) ao banco de dados.

- `SELECT ANY DICTIONARY`  
  Necessário para consultar as tabelas de dicionário do sistema (por exemplo, `SYS.MLOG$` ) para descobrir todos os objetos.

Isso permitirá que o SSMA carregue todos os objetos no esquema de Propriedade do usuário que está se conectando. Na maioria dos cenários do mundo real, há referências entre esquemas entre procedimentos armazenados e o SSMA precisará ser capaz de descobrir todos os objetos referenciados para uma conversão bem-sucedida. Para obter metadados para objetos definidos em outros esquemas, a conta deve ter as seguintes permissões adicionais:

- `SELECT ANY TABLE`  
  Necessário para descobrir tabelas, exibições, exibições materializadas e sinônimos em outros esquemas.

- `SELECT ANY SEQUENCE`  
  Necessário para descobrir sequências em outros esquemas.

- `CREATE ANY PROCEDURE`  
  Necessário para descobrir PL/SQL para procedimentos, funções e pacotes em outros esquemas.

- `CREATE ANY TRIGGER`  
  Necessário para descobrir as definições de gatilho em outros esquemas.

- `CREATE ANY TYPE`  
  Necessário para descobrir tipos definidos em outros esquemas.

Alguns dos recursos do SSMA exigem permissões adicionais. Por exemplo, se você quiser usar a funcionalidade de [Gerenciamento de backup](managing-backups-oracletosql.md) e [testador](testing-migrated-database-objects-oracletosql.md) , será necessário conceder ao usuário de conexão o seguinte:

- `EXECUTE ANY PROCEDURE`  
  Necessário para executar procedimentos e funções que você gostaria de testar em todos os esquemas.

- `CREATE ANY TABLE` e `ALTER ANY TABLE`  
  Necessário para criar e modificar tabelas temporárias para controle de alterações e backups.

- `INSERT ANY TABLE` e `UPDATE ANY TABLE`  
  Necessário para inserir o controle de alterações e os dados de backup em tabelas temporárias.

- `DROP ANY TABLE`  
  Necessário para descartar tabelas temporárias usadas para o controle de alterações e backups.

- `CREATE ANY INDEX` e `ALTER ANY INDEX`  
  Necessário para criar e modificar índices em tabelas temporárias usadas para o controle de alterações e backups.

- `DROP ANY INDEX`  
  Necessário para descartar índices em tabelas temporárias usadas para backup e controle de alterações.

- `CREATE ANY TRIGGER` e `ALTER ANY TRIGGER`  
  Necessário para criar e modificar gatilhos temporários usados para o controle de alterações.

- `DROP ANY TRIGGER`  
  Necessário para descartar gatilhos temporários usados para o controle de alterações.

> [!NOTE]
> Esse é um conjunto genérico de permissões necessárias para que o SSMA opere corretamente. Se você quiser restringir o escopo de sua migração para um subconjunto de esquemas, poderá fazer isso concedendo permissões acima ao conjunto limitado de objetos, em vez de `ALL` . Embora seja possível, pode ser muito difícil identificar corretamente todas as dependências, impedindo que o SSMA funcione corretamente. É altamente recomendável aderir ao conjunto genérico, conforme definido acima, para eliminar quaisquer possíveis problemas de permissão durante o processo de migração.

## <a name="establishing-a-connection-to-oracle"></a>Estabelecendo uma conexão com o Oracle

Quando você se conecta a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando convertem objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e quando migra dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode procurar esses metadados no painel do Gerenciador de metadados Oracle e examinar as propriedades de objetos de banco de dados individuais.

> [!IMPORTANT]
> Antes de tentar se conectar, verifique se o servidor de banco de dados está em execução e pode aceitar conexões.

**Para se conectar ao Oracle**

1. No menu **arquivo** , selecione **conectar-se ao Oracle**.  
   Se você se conectou anteriormente ao Oracle, o nome do comando será **reconectado ao Oracle**.
  
2. Na caixa **provedor** , selecione **provedor de cliente Oracle** ou **provedor de OLE DB**, dependendo de qual provedor está instalado. O padrão é Oracle Client.

3. Na caixa **modo** , selecione o modo **padrão**, **modo TNSNAME**ou modo de **cadeia de conexão**.  
   Use o modo padrão para especificar o nome do servidor e a porta. Use o modo de nome de serviço para especificar manualmente o nome do serviço Oracle. Use o modo de cadeia de conexão para fornecer uma cadeia de conexão completa.

4. Se você selecionar **modo padrão**, forneça os seguintes valores:
   1. Na caixa **nome do servidor** , digite ou selecione o nome ou endereço IP do servidor de banco de dados.
   2. Se o servidor de banco de dados não estiver configurado para aceitar conexões na porta padrão (1521), insira o número da porta que é usado para conexões Oracle na caixa **porta do servidor** .
   3. Na caixa **SID do Oracle** , insira o identificador do sistema.
   4. Na caixa **nome de usuário** , insira uma conta Oracle que tenha as permissões necessárias.
   5. Na caixa **senha** , digite a senha para o nome de usuário especificado.

5. Se você selecionar o **modo TNSNAME**, forneça os seguintes valores:
   1. Na caixa **identificador de conexão** , insira o identificador de conexão (alias TNS) do banco de dados.
   2. Na caixa **nome de usuário** , insira uma conta Oracle que tenha as permissões necessárias.
   3. Na caixa **senha** , digite a senha para o nome de usuário especificado.
  
6. Se você selecionar **modo de cadeia de conexão**, forneça uma cadeia de conexão na caixa **cadeia de conexão** .  
   O exemplo a seguir mostra uma cadeia de conexão OLE DB:

   `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`

   O exemplo a seguir mostra uma cadeia de conexão do cliente Oracle que usa segurança integrada:

   `Data Source=MyOracleDB;Integrated Security=yes;`

   Para obter mais informações, consulte [conectar-se ao Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).

## <a name="reconnecting-to-oracle"></a>Reconectando ao Oracle

A conexão com o servidor de banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados. Você pode trabalhar offline até que queira atualizar os metadados, carregar objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados no e migrar os mesmos.

## <a name="refreshing-oracle-metadata"></a>Atualizando metadados do Oracle

Os metadados sobre o banco de dados Oracle não são atualizados automaticamente. Os metadados no Gerenciador de metadados Oracle são um instantâneo dos metadados quando você se conectou pela primeira vez ou na última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os esquemas, um único esquema ou objetos de banco de dados individuais.

**Para atualizar metadados**

1. Certifique-se de que você está conectado ao banco de dados.

2. No Gerenciador de metadados Oracle, marque a caixa de seleção ao lado de cada esquema ou objeto de banco de dados que você deseja atualizar.

3. Clique com o botão direito do mouse em **esquemas**ou o esquema individual ou objeto de banco de dados e selecione **Atualizar do banco de dados**.  
   Se você não tiver uma conexão ativa, o SSMA exibirá a caixa de diálogo **conectar ao Oracle** para que você possa se conectar.

4. Na caixa de diálogo atualizar do banco de dados, especifique quais objetos atualizar.

   - Para atualizar um objeto, clique no campo **ativo** adjacente ao objeto até que uma seta seja exibida.
   - Para impedir que um objeto seja atualizado, clique no campo **ativo** adjacente ao objeto até que um **X** seja exibido.
   - Para atualizar ou recusar uma categoria de objetos, clique no campo **ativo** adjacente à pasta Category.

   Para exibir as definições da codificação de cores, clique no botão **legenda** .

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]

## <a name="next-steps"></a>Próximas etapas

A próxima etapa do processo de migração é [conectar-se a uma instância do SQL Server](connecting-to-sql-server-oracletosql.md).

## <a name="see-also"></a>Veja também

[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
