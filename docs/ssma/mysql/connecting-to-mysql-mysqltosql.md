---
title: Conectando-se ao MySQL (MySQLToSQL) | Microsoft Docs
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
ms.openlocfilehash: 6cb47c0f06d7133b8c7454a4fa538937a0e78e19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103167"
---
# <a name="connecting-to-mysql-mysqltosql"></a>Conectar-se ao MySQL (MySQLToSQL)
Para migrar bancos de dados MySQL para SQL Server ou SQL Azure, você deve se conectar ao banco de dados MySQL que deseja migrar. Quando você se conecta, o SSMA obtém metadados sobre todos os esquemas do MySQL e, em seguida, exibe-os no painel do Gerenciador de metadados do MySQL. O SSMA armazena informações sobre o servidor de banco de dados, mas não armazena senhas.  
  
A conexão com o banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados.  
  
Os metadados sobre o banco de dados MySQL não são atualizados automaticamente. Em vez disso, se você quiser atualizar os metadados no Gerenciador de metadados do MySQL, você deve atualizá-lo manualmente. Para obter mais informações, consulte a seção "Atualizando metadados do MySQL" mais adiante neste tópico.  
  
## <a name="required-mysql-permissions"></a>Permissões do MySQL necessárias  
A conta usada para conectar-se ao banco de dados MySQL deve ter pelo menos permissões de **conexão** . Isso permite que o SSMA obtenha metadados de esquemas de Propriedade do usuário que está se conectando. Para obter metadados de objetos em outros esquemas e, em seguida, converter objetos nesses esquemas, a conta deve ter as seguintes permissões:  
  
-   Privilégios ' SHOW ' em objetos de banco de dados  
  
-   Privilégio ' SELECT ' em ' Information_schema '  
  
-   Privilégio "SELECT" no MySQL (para UDFs)  
  
## <a name="establishing-a-connection-to-mysql"></a>Estabelecendo uma conexão com o MySQL  
Quando você se conecta a um banco de dados, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados são usados pelo SSMA quando convertem objetos em SQL Server ou SQL Azure sintaxe e ao migrar dados para SQL Server ou SQL Azure. Você pode procurar esses metadados no painel do explorador de metadados do MySQL e examinar as propriedades de objetos de banco de dados individuais.  
  
> [!IMPORTANT]  
> Antes de tentar se conectar, verifique se o servidor de banco de dados está em execução e pode aceitar conexões.  
  
**Para se conectar ao MySQL**  
  
1.  No menu **arquivo** , selecione **conectar-se ao MySQL** (essa opção será habilitada após a criação do projeto).  
  
    Se você estiver conectado anteriormente ao MySQL, o nome do comando será **reconectado ao MySQL**.  
  
2.  Na caixa **provedor** , selecione MySQL ODBC 5,1 driver (confiável). É o provedor padrão no modo padrão.  
  
3.  Na caixa **modo** , selecione **modo padrão**. Esse é o modo padrão.  
  
    Use o modo padrão para especificar o nome do servidor e a porta.  
  
4.  No **modo padrão**, forneça os seguintes valores:  
  
    1.  Na caixa **nome do servidor** , digite o nome do servidor MySQL. Na caixa **porta do servidor** , digite o número da porta a ser 3306. É a porta padrão.  
  
    2.  Na caixa **nome de usuário** , insira uma conta do MySQL que tenha as permissões necessárias.  
  
    3.  Na caixa **senha** , digite a senha para o nome de usuário especificado.  
  
5.  **SSL:** Se você quiser se conectar com segurança ao MySQL, faça o uso da SSL (Secure Socket Layer) marcando a caixa de seleção **SSL** .  
  
6.  **Configurar:** Ele fornece uma opção para configurar a conexão com o MySQL por meio do protocolo SSL.  
  
    > [!NOTE]  
    > Para habilitar **Configurar**, o SSL deve ser definido como **true**.  
  
    Ao clicar no botão "configurar", uma caixa de diálogo é exibida. Para usar a criptografia ao se conectar ao banco de dados MySQL, o caminho para os três arquivos de certificado a seguir presentes na caixa de diálogo deve ser definido [certificados de Privacy Enhanced Mail (PEM)]:  
  
    -   **Autoridade de certificação SSL:** Especifica o caminho para um arquivo com uma lista de autoridades de certificação SSL de confiança.  
  
    -   **Certificado SSL:** Especifica o nome do arquivo de certificado SSL a ser usado para estabelecer uma conexão segura.  
  
    -   **chave SSL:** Especifica o nome do arquivo de chave SSL a ser usado para estabelecer uma conexão segura.  
  
    > [!NOTE]  
    > -   O botão **OK** é habilitado quando as informações necessárias foram fornecidas. Se qualquer um dos caminhos de arquivo for inválido, o botão "OK" permanecerá desabilitado.  
    > -   O botão **Cancelar** fecha a caixa de diálogo e **DESATIVA** a opção SSL do formulário de conexão principal.  
  
7.  Para obter mais informações, consulte [conectar-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>Reconectando ao MySQL  
A conexão com o servidor de banco de dados permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar se quiser uma conexão ativa com o banco de dados. Você pode trabalhar offline até que queira atualizar metadados, carregar objetos de banco de dados em SQL Server ou SQL Azure e migrar dados.  
  
## <a name="refreshing-mysql-metadata"></a>Atualizando metadados do MySQL  
Os metadados sobre o banco de dados MySQL não são atualizados automaticamente. Os metadados no Gerenciador de metadados do MySQL são um instantâneo dos metadados quando você se conecta pela primeira vez ou na última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os esquemas, um único esquema ou objetos de banco de dados individuais.  
  
**Para atualizar metadados**  
  
1.  Certifique-se de que você está conectado ao banco de dados.  
  
2.  No Gerenciador de metadados do MySQL, marque a caixa de seleção ao lado de cada esquema ou objeto de banco de dados que você deseja atualizar.  
  
3.  Clique com o botão direito do mouse em **esquemas**ou o esquema individual ou objeto de banco de dados e selecione **Atualizar do banco de dados**.  
  
    Se você não tiver uma conexão ativa, o SSMA exibirá a caixa de diálogo **conectar ao MySQL** para que você possa se conectar.  
  
4.  Na caixa de diálogo atualizar do banco de dados, especifique quais objetos atualizar.  
  
    -   Para atualizar um objeto, clique no campo **ativo** adjacente ao objeto até que uma seta seja exibida.  
  
    -   Para impedir que um objeto seja atualizado, clique no campo **ativo** adjacente ao objeto até que um **X** seja exibido.  
  
    -   Para atualizar ou recusar uma categoria de objetos, clique no campo **ativo** adjacente à pasta Category.  
  
    -   Para exibir as definições da codificação de cores, clique no botão **legenda** .  
  
5.  Clique em **OK**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração está [se conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
