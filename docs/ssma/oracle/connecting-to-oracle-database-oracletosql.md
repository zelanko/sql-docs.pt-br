---
title: Conectar-se ao banco de dados Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6a4ac43e0f79e8f7841f8f9d4234ccdd988a7b6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-oracle-database-oracletosql"></a>Conectar-se ao banco de dados Oracle (OracleToSQL)
Para migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve se conectar ao banco de dados Oracle que você deseja migrar. Quando você se conectar, o SSMA obtém metadados sobre todos os esquemas do Oracle e exibe no painel Explorador de metadados do Oracle. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena as senhas.  
  
Sua conexão ao banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar se você quiser uma conexão ativa com o banco de dados.  
  
Metadados sobre o banco de dados Oracle não é atualizado automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do Oracle, você deve atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualização de metadados do Oracle" mais adiante neste tópico.  
  
## <a name="required-oracle-permissions"></a>Permissões necessárias do Oracle  
A conta que é usada para se conectar ao banco de dados Oracle deve ter pelo menos **conectar** permissões. Isso permite que o SSMA obter metadados de esquemas de propriedade do usuário conectado. Para obter metadados para objetos em outros esquemas e, em seguida, converter objetos nesses esquemas, a conta deve ter as seguintes permissões:  
  
-   CRIE QUALQUER PROCEDIMENTO  
  
-   EXECUTAR NENHUM PROCEDIMENTO  
  
-   SELECIONE QUALQUER TABELA  
  
-   SELECIONE QUALQUER SEQUÊNCIA  
  
-   CRIAR QUALQUER TIPO  
  
-   CRIAR QUALQUER GATILHO  
  
-   SELECIONE QUALQUER DICIONÁRIO  
  
## <a name="establishing-a-connection-to-oracle"></a>Estabelecer uma Conexão para Oracle  
Quando você se conectar a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando ele converte objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe, e quando ele migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode procurar esses metadados no painel Explorador de metadados do Oracle e examine as propriedades dos objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar, certifique-se de que o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para se conectar ao Oracle**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao Oracle**.  
  
    Se você se conectado anteriormente ao Oracle, o nome do comando será **reconectar-se ao Oracle**.  
  
2.  No **provedor** selecione **provedor de cliente Oracle** ou **provedor OLE DB**, dependendo de qual provedor está instalado. O padrão é o cliente Oracle.  
  
3.  No **modo** , selecione o **modo padrão**, **modo TNSNAME**, ou **modo de cadeia de caracteres de Conexão**.  
  
    Use o modo padrão para especificar o nome do servidor e a porta. Use o modo de nome de serviço para especificar o nome do serviço Oracle manualmente. Use o modo de cadeia de caracteres de conexão para fornecer uma cadeia de caracteres de conexão completa.  
  
4.  Se você selecionar **modo padrão**, forneça os seguintes valores:  
  
    1.  No **nome do servidor** caixa, digite ou selecione o nome ou endereço IP do servidor de banco de dados.  
  
    2.  Se o servidor de banco de dados não está configurado para aceitar conexões em padrão (1521) de porta, digite o número da porta que é usado para conexões Oracle no **porta do servidor** caixa.  
  
    3.  No **Oracle SID** , digite o identificador do sistema.  
  
    4.  No **nome de usuário** , digite uma conta de Oracle que tenha as permissões necessárias.  
  
    5.  No **senha** , digite a senha para o nome de usuário especificado.  
  
5.  Se você selecionar **modo TNSNAME**, forneça os seguintes valores:  
  
    1.  No **conectar identificador** , digite conectar-se o identificador (alias TNS) do banco de dados.  
  
    2.  No **nome de usuário** , digite uma conta de Oracle que tenha as permissões necessárias.  
  
    3.  No **senha** , digite a senha para o nome de usuário especificado.  
  
6.  Se você selecionar **modo de cadeia de caracteres de Conexão**, forneça uma cadeia de conexão no **cadeia de caracteres de Conexão** caixa.  
  
    O exemplo a seguir mostra uma cadeia de caracteres de conexão OLE DB:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    O exemplo a seguir mostra uma cadeia de caracteres de conexão de cliente Oracle que usa segurança integrada:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Para obter mais informações, consulte [conectar-se ao Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Reconectar-se ao Oracle  
Sua conexão com o servidor de banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar se você quiser uma conexão ativa com o banco de dados. Você pode trabalhar offline até que você deseja atualizar os metadados, carregue os objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e migrar dados.  
  
## <a name="refreshing-oracle-metadata"></a>Atualizar metadados do Oracle  
Metadados sobre o banco de dados Oracle não será atualizado automaticamente. Os metadados no Gerenciador de metadados do Oracle são um instantâneo de metadados quando conectado pela primeira vez ou a última vez que você atualizou metadados manualmente. Você pode atualizar manualmente os metadados para todos os esquemas, um único esquema ou objetos de banco de dados individuais.  
  
**Para atualizar metadados**  
  
1.  Certifique-se de que você está conectado ao banco de dados.  
  
2.  No Gerenciador de metadados do Oracle, selecione a caixa de seleção ao lado de cada objeto de esquema ou banco de dados que você deseja atualizar.  
  
3.  Clique com botão direito **esquemas**, ou o esquema individual ou o banco de dados do objeto e, em seguida, selecione **de atualização do banco de dados**.  
  
    Se você não tiver uma conexão ativa, o SSMA exibirá o **conectar-se ao Oracle** caixa de diálogo para que você pode se conectar.  
  
4.  Na atualização da caixa de diálogo banco de dados, especifique quais objetos para atualização.  
  
    -   Para atualizar um objeto, clique o **Active** campo adjacente ao objeto até que uma seta é exibida.  
  
    -   Para impedir que um objeto que está sendo atualizado, clique no **Active** campo adjacente ao objeto até um **X** é exibida.  
  
    -   Para atualizar ou recusar uma categoria de objetos, clique no **Active** campo adjacente à pasta de categoria.  
  
    Para exibir as definições de codificação de cores, clique o **legenda** botão.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>Próxima etapa  
  
-   A próxima etapa no processo de migração é [conectar-se a uma instância do SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

