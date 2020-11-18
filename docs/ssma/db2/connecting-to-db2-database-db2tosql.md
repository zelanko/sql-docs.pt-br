---
title: Conectando-se ao banco de dados DB2 (DB2ToSQL) | Microsoft Docs
description: Saiba como se conectar a uma instância de destino do banco de dados DB2 para migrar bancos de dados DB2. O SSMA obtém metadados sobre todos os esquemas do DB2.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d0ac703c8ea155f33ecb713b98a26f0c39b5a695
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870065"
---
# <a name="connecting-to-db2-database-db2tosql"></a>Conectando-se ao banco de dados DB2 (DB2ToSQL)

Para migrar bancos de dados DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar ao banco de dados DB2 que deseja migrar. Quando você se conecta, o SSMA obtém metadados sobre todos os esquemas do DB2 e, em seguida, exibe-os no painel do Gerenciador de metadados do DB2. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena senhas.

A conexão com o banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados.

Os metadados sobre o banco de dados DB2 não são atualizados automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do DB2, será necessário atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualizando metadados do DB2" mais adiante neste tópico.

## <a name="required-db2-permissions"></a>Permissões do DB2 necessárias

A autorização do usuário define a lista de comandos e objetos que estão disponíveis para um usuário. Assim, essa lista controla as ações do usuário. No DB2, há grupos de privilégios predeterminados para autorização, tanto no nível da instância quanto no nível de um banco de dados DB2. Isso permite que o SSMA obtenha metadados de esquemas de Propriedade do usuário que está se conectando. Para obter metadados de objetos em outros esquemas e, em seguida, converter objetos nesses esquemas, a conta deve ter as seguintes permissões:

- O acesso ao esquema para migração de esquema normalmente é concedido a público, a menos que a palavra-chave restrict tenha sido usada na criação
- O acesso a dados para migração de dados requer o acesso ao DataAccess

## <a name="establishing-a-connection-to-db2"></a>Estabelecendo uma conexão com o DB2

Quando você se conecta a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando convertem objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e quando migra dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode procurar esses metadados no painel do Gerenciador de metadados do DB2 e examinar as propriedades de objetos de banco de dados individuais.  

> [!IMPORTANT]
> Antes de tentar se conectar, verifique se o servidor de banco de dados está em execução e pode aceitar conexões.

**Para se conectar ao DB2**

1. No menu **arquivo** , selecione **conectar-se ao DB2**.

   Se você se conectou anteriormente ao DB2, o nome do comando será **reconectado ao DB2**.

2. Na caixa **provedor** , você verá o **provedor de OLE DB** que atualmente é o único provedor de acesso para cliente DB2.

3. Na caixa **Gerenciador** , você pode selecionar **DB2 para zOs**, **DB2 para LUW** ou **DB2 para i**

4. Na caixa **modo** , selecione o modo **padrão** ou o **modo de cadeia de conexão**.

   Use o modo padrão para especificar o nome do servidor e a porta. Use o modo de nome de serviço para especificar manualmente o nome do serviço DB2. Use o modo de cadeia de conexão para fornecer uma cadeia de conexão completa.

5. Se você selecionar **modo padrão**, forneça os seguintes valores:

   - Na caixa **nome do servidor** , digite ou selecione o nome ou endereço IP do servidor de banco de dados.
   - Se o servidor de banco de dados não estiver configurado para aceitar conexões na porta padrão (1521), insira o número da porta que é usado para conexões DB2 na caixa **porta do servidor** .
   - Na caixa **porta do servidor** , digite o número da porta TCP/IP.
   - Na caixa **catálogo inicial** , insira o nome do banco de dados.
   - Na caixa **nome de usuário** , insira uma conta do DB2 que tenha as permissões necessárias.
   - Na caixa **senha** , digite a senha para o nome de usuário especificado.

6. Se você selecionar **modo de cadeia de conexão**, forneça uma cadeia de conexão na caixa **cadeia de conexão** .

   O exemplo a seguir mostra uma cadeia de conexão OLE DB:

   `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`

   O exemplo a seguir mostra uma cadeia de conexão do cliente DB2 que usa segurança integrada:
  
   `Data Source=MyDB2DB;Integrated Security=yes;`

   Para obter mais informações, consulte [conectar-se ao Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).
  
## <a name="reconnecting-to-db2"></a>Reconectando ao DB2

A conexão com o servidor de banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados. Você pode trabalhar offline até que queira atualizar os metadados, carregar objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados no e migrar os mesmos.

## <a name="refreshing-db2-metadata"></a>Atualizando metadados do DB2

Os metadados sobre o banco de dados DB2 não são atualizados automaticamente. Os metadados no Gerenciador de metadados do DB2 são um instantâneo dos metadados quando você se conecta pela primeira vez ou a última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os esquemas, um único esquema ou objetos de banco de dados individuais.

**Para atualizar metadados**

1. Certifique-se de que você está conectado ao banco de dados.
2. No Gerenciador de metadados do DB2, marque a caixa de seleção ao lado de cada esquema ou objeto de banco de dados que você deseja atualizar.
3. Clique com o botão direito do mouse em **esquemas** ou o esquema individual ou objeto de banco de dados e selecione **Atualizar do banco de dados**.

   Se você não tiver uma conexão ativa, o SSMA exibirá a caixa de diálogo **conectar ao DB2** para que você possa se conectar.
  
4. Na caixa de diálogo atualizar do banco de dados, especifique quais objetos atualizar.
   - Para atualizar um objeto, clique no campo **ativo** adjacente ao objeto até que uma seta seja exibida.
   - Para impedir que um objeto seja atualizado, clique no campo **ativo** adjacente ao objeto até que um **X** seja exibido.
   - Para atualizar ou recusar uma categoria de objetos, clique no campo **ativo** adjacente à pasta Category.

     Para exibir as definições da codificação de cores, clique no botão **legenda** .

5. [!INCLUDE[click OK](../../includes/clickok-md.md)]

## <a name="next-step"></a>Próxima etapa

- A próxima etapa do processo de migração é [conectar-se a SQL Server](./connecting-to-sql-server-db2tosql.md).

## <a name="see-also"></a>Consulte Também

- [Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)