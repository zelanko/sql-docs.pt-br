---
title: Conectar-se ao MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 233b6824ef527a9ed4e7e02164a08e31e41f3699
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253333"
---
# <a name="connecting-to-mysql-mysqltosql"></a>Conectar-se ao MySQL (MySQLToSQL)
Para migrar bancos de dados MySQL para o SQL Server ou SQL Azure, você deve se conectar ao banco de dados MySQL que você deseja migrar. Quando você se conecta, SSMA obtém metadados sobre todos os esquemas de MySQL e depois o exibe no painel Gerenciador de metadados do MySQL. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena as senhas.  
  
Sua conexão ao banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar se você quiser que uma conexão ativa para o banco de dados.  
  
Metadados sobre o banco de dados MySQL não é atualizado automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do MySQL, você deve atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualizando metadados do MySQL" mais adiante neste tópico.  
  
## <a name="required-mysql-permissions"></a>Permissões necessárias do MySQL  
A conta que é usada para se conectar ao banco de dados MySQL deve ter pelo menos **CONNECT** permissões. Isso permite que o SSMA obter metadados de esquemas de propriedade do usuário está se conectando. Para obter metadados para objetos em outros esquemas e, em seguida, converter objetos nesses esquemas, a conta deve ter as seguintes permissões:  
  
-   'SHOW' privilégios em objetos de banco de dados  
  
-   Privilégio 'SELECT' em 'Information_schema'  
  
-   'SELECT' privilégio no mysql (para UDFs)  
  
## <a name="establishing-a-connection-to-mysql"></a>Estabelecer uma Conexão ao MySQL  
Quando você se conectar a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando ele converte objetos em sintaxe de SQL Server ou SQL Azure, e quando ele migra dados para o SQL Server ou SQL Azure. Você pode procurar esses metadados no painel Gerenciador de metadados do MySQL e examine as propriedades dos objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar, certifique-se de que o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para se conectar ao MySQL**  
  
1.  Sobre o **arquivo** menu, selecione **conectar-se ao MySQL** (essa opção será habilitada após a criação do projeto).  
  
    Se você estiver conectado anteriormente ao MySQL, o nome do comando será **reconectar-se ao MySQL**.  
  
2.  No **provedor** , selecione o Driver 5.1 ODBC do MySQL (confiável). É o provedor padrão no modo padrão.  
  
3.  No **modo** caixa, selecione **modo padrão**. Esse é o modo padrão.  
  
    Use o modo padrão para especificar o nome do servidor e a porta.  
  
4.  Na **o modo padrão**, forneça os seguintes valores:  
  
    1.  No **nome do servidor** , digite o nome do servidor MySQL. No **porta do servidor** , digite o número de porta a ser 3306. É a porta padrão.  
  
    2.  No **nome de usuário** , digite uma conta do MySQL que tem as permissões necessárias.  
  
    3.  No **senha** , digite a senha para o nome de usuário especificado.  
  
5.  **SSL:** Se você quiser se conectar com segurança ao MySQL, certifique-se de usar de Secure Socket Layer (SSL), verificando a **SSL** caixa de seleção.  
  
6.  **Configure:** Ele fornece uma opção para configurar a conexão ao MySQL por meio do Secure Socket Layer (SSL).  
  
    > [!NOTE]  
    > Para habilitar **configurar**, SSL deve ser definida como **verdadeiro**.  
  
    Clicando no botão "Configurar", uma caixa de diálogo é exibida. Para usar a criptografia enquanto se conectar ao banco de dados MySQL, o caminho para os seguintes arquivos de três certificado presentes na caixa de diálogo deve ser definido [privacidade aprimorada Mail certificados (PEM)]:  
  
    -   **Autoridade de certificação SSL:** Especifica o caminho para um arquivo com uma lista de confiança autoridades de certificação SSL.  
  
    -   **Certificado SSL:** Especifica o nome do arquivo de certificado SSL a ser usado para estabelecer uma conexão segura.  
  
    -   **CHAVE SSL:** Especifica o nome do arquivo de chave SSL a ser usado para estabelecer uma conexão segura.  
  
    > [!NOTE]  
    > -   O **Okey** botão é habilitado quando as informações necessárias foram fornecidas. Se qualquer um dos caminhos de arquivo for inválido, o botão "Okey" permanecerá desabilitado.  
    > -   O **cancele** botão fecha a caixa de diálogo e **desativa** a opção SSL do formulário de Conexão principal.  
  
7.  Para obter mais informações, consulte [conectar-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>Reconectar-se ao MySQL  
Sua conexão com o servidor de banco de dados permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar se você quiser que uma conexão ativa para o banco de dados. Você pode trabalhar offline até que você deseja atualizar os metadados, carregar objetos de banco de dados no SQL Server ou SQL Azure e migrar os dados.  
  
## <a name="refreshing-mysql-metadata"></a>Atualizar metadados do MySQL  
Metadados sobre o banco de dados MySQL não é atualizado automaticamente. Os metadados no Gerenciador de metadados do MySQL são um instantâneo dos metadados quando conectado pela primeira vez ou a última vez que você atualizou metadados manualmente. Você pode atualizar manualmente os metadados para todos os esquemas, um único esquema ou objetos de banco de dados individuais.  
  
**Para atualizar os metadados**  
  
1.  Certifique-se de que você está conectado ao banco de dados.  
  
2.  No Gerenciador de metadados do MySQL, selecione a caixa de seleção ao lado de cada objeto de esquema ou banco de dados que você deseja atualizar.  
  
3.  Clique com botão direito **esquemas**, ou o esquema individual ou o banco de dados de objeto e, em seguida, selecione **atualização do banco de dados**.  
  
    Se você não tiver uma conexão ativa, o SSMA exibirá os **conectar-se ao MySQL** caixa de diálogo para que você pode se conectar.  
  
4.  Na atualização da caixa de diálogo banco de dados, especifica quais objetos a ser atualizada.  
  
    -   Para atualizar um objeto, clique o **Active** campo adjacente ao objeto até que uma seta é exibida.  
  
    -   Para impedir que um objeto que está sendo atualizado, clique no **Active** campo adjacente ao objeto até um **X** é exibida.  
  
    -   Para atualizar ou recusar uma categoria de objetos, clique no **Active** campo adjacente para a pasta de categoria.  
  
    -   Para exibir as definições de codificação de cores, clique o **legenda** botão.  
  
5.  Clique em **OK**.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
