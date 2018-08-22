---
title: Conectar-se ao banco de dados do DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2228a08c2985f4e683ff860cd77e68159a0ecd0a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396210"
---
# <a name="connecting-to-db2-database-db2tosql"></a>Conectar-se ao banco de dados do DB2 (DB2ToSQL)
Migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve se conectar ao banco de dados DB2 que você deseja migrar. Quando você se conectar, o SSMA obtém metadados sobre todos os esquemas do DB2 e depois o exibe no painel Gerenciador de metadados do DB2. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena as senhas.  
  
Sua conexão ao banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar se você quiser que uma conexão ativa para o banco de dados.  
  
Metadados sobre o banco de dados do DB2 não é atualizado automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do DB2, você deve atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualizando metadados do DB2" mais adiante neste tópico.  
  
## <a name="required-db2-permissions"></a>Permissões necessárias do DB2  
Autorização de usuário define a lista dos comandos e objetos que estão disponíveis para um usuário. Essa lista, assim, controla as ações do usuário. No DB2, há grupos predeterminados de privilégios para autorização, no nível de instância e no nível de um banco de dados do DB2. Isso permite que o SSMA obter metadados de esquemas de propriedade do usuário está se conectando. Para obter metadados para objetos em outros esquemas e, em seguida, converter objetos nesses esquemas, a conta deve ter as seguintes permissões:  
  
-   Acesso de esquema para a migração de esquema normalmente é concedido a público, a menos que a palavra-chave RESTRICT foi usada na criação  
  
-   Acesso a dados para migração de dados requer DATAACCESS  
  
## <a name="establishing-a-connection-to-db2"></a>Estabelecer uma Conexão para o DB2  
Quando você se conectar a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando ele converte objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, e quando ele migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode procurar esses metadados no painel Gerenciador de metadados do DB2 e examine as propriedades dos objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar, certifique-se de que o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para se conectar ao DB2**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao DB2**.  
  
    Se você se conectado anteriormente ao DB2, o nome do comando será **reconectar-se ao DB2**.  
  
2.  No **provedor** caixa, você verá o **OLE DB Provider** que atualmente é o único provedor de acesso de cliente do DB2.  
  
3.  No **Manager** caixa, você pode selecionar um **Db2 para zOs**, ou **DB2 para LUW**  
  
4.  No **modo** , selecione qualquer uma **modo padrão**, ou **modo de cadeia de caracteres de Conexão**.  
  
    Use o modo padrão para especificar o nome do servidor e a porta. Use o modo de nome de serviço para especificar o nome do serviço DB2 manualmente. Use o modo de cadeia de caracteres de conexão para fornecer uma cadeia de conexão completa.  
  
5.  Se você selecionar **o modo padrão**, forneça os seguintes valores:  
  
    -   No **nome do servidor** caixa, digite ou selecione o nome ou endereço IP do servidor de banco de dados.  
  
    -   Se o servidor de banco de dados não estiver configurado para aceitar conexões no padrão da porta (1521), insira o número da porta que é usado para conexões do DB2 na **porta do servidor** caixa.  
  
    -   No **porta do servidor** , digite o número da porta TCP/IP.  
  
    -   No **Initial Catalog** , digite o nome do banco de dados  
  
    -   No **nome de usuário** , digite uma conta do DB2 que tem as permissões necessárias.  
  
    -   No **senha** , digite a senha para o nome de usuário especificado.  
  
6.  Se você selecionar **modo de cadeia de caracteres de Conexão**, forneça uma cadeia de conexão na **cadeia de caracteres de Conexão** caixa.  
  
    O exemplo a seguir mostra uma cadeia de caracteres de conexão do OLE DB:  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    O exemplo a seguir mostra uma cadeia de caracteres de conexão de cliente DB2 que usa segurança integrada:  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    Para obter mais informações, consulte [conectar-se ao Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-db2"></a>Reconectar-se ao DB2  
Sua conexão com o servidor de banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar se você quiser que uma conexão ativa para o banco de dados. Você pode trabalhar offline até que você deseja atualizar os metadados, carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e migrar dados.  
  
## <a name="refreshing-db2-metadata"></a>Atualizar metadados do DB2  
Metadados sobre o banco de dados do DB2 não é atualizado automaticamente. Os metadados no Gerenciador de metadados do DB2 são um instantâneo dos metadados quando conectado pela primeira vez ou a última vez que você atualizou metadados manualmente. Você pode atualizar manualmente os metadados para todos os esquemas, um único esquema ou objetos de banco de dados individuais.  
  
**Para atualizar os metadados**  
  
1.  Certifique-se de que você está conectado ao banco de dados.  
  
2.  No Gerenciador de metadados do DB2, selecione a caixa de seleção ao lado de cada objeto de esquema ou banco de dados que você deseja atualizar.  
  
3.  Clique com botão direito **esquemas**, ou o esquema individual ou o banco de dados de objeto e, em seguida, selecione **atualização do banco de dados**.  
  
    Se você não tiver uma conexão ativa, o SSMA exibirá os **conectar-se ao DB2** caixa de diálogo para que você pode se conectar.  
  
4.  Na atualização da caixa de diálogo banco de dados, especifica quais objetos a ser atualizada.  
  
    -   Para atualizar um objeto, clique o **Active** campo adjacente ao objeto até que uma seta é exibida.  
  
    -   Para impedir que um objeto que está sendo atualizado, clique no **Active** campo adjacente ao objeto até um **X** é exibida.  
  
    -   Para atualizar ou recusar uma categoria de objetos, clique no **Active** campo adjacente para a pasta de categoria.  
  
    Para exibir as definições de codificação de cores, clique o **legenda** botão.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>Próxima etapa  
  
-   É a próxima etapa no processo de migração [conectando ao SQL Server](http://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados do DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
