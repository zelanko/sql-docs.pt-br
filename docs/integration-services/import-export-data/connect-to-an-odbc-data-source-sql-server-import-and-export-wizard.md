---
title: Conectar-se a uma fonte de dados do ODBC (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
description: Como configurar um DSN ODBC ou criar uma cadeia de conexão ODBC para usar com o Assistente de Importação e Exportação do SQL Server
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 73259121c31fcfc74352bf47938fcf28b294b894
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773582"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do ODBC (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tópico mostra como se conectar a uma fonte de dados do **ODBC** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server.

Talvez você precise baixar o driver ODBC do qual você precisa da Microsoft ou de terceiros.

Você também pode ter que pesquisar as informações de conexão necessárias que você precisa fornecer. Esse site de terceiros – [The Connection Strings Reference](https://www.connectionstrings.com/) (A Referência de Cadeias de Conexão) – contém cadeias de conexão de exemplo e mais informações sobre provedores de dados e as informações de conexão exigidas por eles.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Verifique se o driver que você deseja está instalado
1.  Pesquise pelo miniaplicativo **fontes de dados ODBC (64 bits)** ou navegue até ele no Menu Iniciar ou Painel de Controle. Se você só tem um driver de 32 bits ou você sabe que precisa usar um driver de 32 bits, em vez disso, pesquise pelas **Fontes de Dados ODBC (32 bits)** ou navegue até elas.
2.  Inicie o miniaplicativo. A janela **Administrador de Fonte de Dados ODBC** se abre.
3.  Na guia **Drivers**, você pode encontrar uma lista de todos os drivers ODBC instalados no seu computador. (Os nomes de alguns dos drivers podem estar listados em vários idiomas.)

    Aqui está um exemplo da lista de drivers de 64 bits instalados.

    ![Drivers ODBC de 64 bits instalados](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Se você sabe que o driver está instalado e você não o vê no miniaplicativo de 64 bits, procure-o no miniaplicativo de 32 bits. Isso também indica se é necessário executar o Assistente de Importação e Exportação do SQL Server de 32 ou 64 bits.
>
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.
    
## <a name="step-1---select-the-data-source"></a>Etapa 1 – selecionar a fonte de dados
Os drivers ODBC instalados em seu computador não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **Provedor de Dados do .NET Framework para ODBC** como a fonte de dados na página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do assistente. Esse provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o Provedor de Dados do .NET Framework para ODBC.

![Conectar-se ao SQL com o ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Etapa 2 – fornecer as informações de conexão
A próxima etapa é fornecer as informações de conexão para o driver ODBC e sua fonte de dados. Você tem duas opções.
1.  Forneça um **DSN** (nome de fonte de dados) que já exista ou que você crie com o miniaplicativo **Administrador de fonte de dados ODBC**. Um DSN é a coleção salva de configurações necessárias para se conectar a uma fonte de dados ODBC.

    Se você já conhece o nome DSN ou sabe como criar um novo DSN agora, você pode ignorar o restante desta página. Digite o nome DSN no campo **Dsn** na página **Escolher uma fonte de dados** ou **Escolher um destino** e continue para a próxima etapa do assistente.

    [Fornecer um DSN](#odbc_dsn)
    
2.  Forneça uma **cadeia de conexão**, que você pode pesquisar online ou então criar e testar em seu computador com o miniaplicativo **Administrador de Fonte de Dados ODBC**.

    Se você já tem a cadeia de conexão ou sabe como criá-la, você pode ignorar o restante desta página. Digite a cadeia de conexão no campo **ConnectionString** na página **Escolher uma fonte de dados** ou **Escolher um destino** e continue para a próxima etapa do assistente.

    [Fornecer uma cadeia de conexão](#odbc_connstring)

Se você fornecer uma cadeia de conexão, a página **Escolher uma fonte de dados** ou **Escolher um destino** exibe todas as informações de conexão que o assistente usará para se conectar à fonte de dados, tais como o método de autenticação e nome do servidor e banco de dados. Se você fornecer um DSN, essas informações não estarão visíveis.

## <a name="option-1---provide-a-dsn"></a><a name="odbc_dsn"></a> Opção 1 – fornecer um DSN
Se você quiser fornecer as informações de conexão com um DSN (nome de fonte de dados), use o miniaplicativo **Administrador de Fonte de Dados ODBC** para localizar o DSN existente ou criar um novo.
1.  Pesquise pelo miniaplicativo **fontes de dados ODBC (64 bits)** ou navegue até ele no Menu Iniciar ou Painel de Controle. Se você só tem um driver de 32 bits ou deve usar um driver de 32 bits, em vez disso, pesquise pelas **Fontes de Dados ODBC (32 bits)** ou navegue até elas.
2.  Inicie o miniaplicativo. A janela **Administrador de Fonte de Dados ODBC** se abre. Eis aqui a aparência desse miniaplicativo.

    ![Miniaplicativo de painel de controle do Administrador de ODBC](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Se você quiser **Usar um DSN existente** para sua fonte de dados, você poderá usar qualquer DSN que você vir na guia **DSN do Usuário**, **DSN de Sistema** ou **DSN de Arquivo**. Verifique o nome e então retorne para o assistente e insira-o no campo **Dsn** na página **Escolher uma fonte de dados** ou **Escolher um destino**. Ignore o restante desta página e continue para a próxima etapa do assistente.
4.  Se você quiser **criar um novo DSN**, decida se você deseja que ele fique visível apenas para você (DSN do usuário), visível para todos os usuários do computador incluindo serviços Windows (DSN de Sistema) ou salvos em um arquivo (DSN de Arquivo). Este exemplo cria um novo DSN de Sistema.
5. Na guia **DSN de Sistema**, clique em **Adicionar**.

    ![Adicionar um novo DSN de sistema ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  Na caixa de diálogo **Criar uma Nova Fonte de Dados**, selecione o driver para a fonte de dados e clique em **Concluir**.

    ![Escolher o driver para o DSN de sistema](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. O driver agora exibe uma ou mais telas específicas de driver em que você insere as informações necessárias para se conectar à fonte de dados. (Para o driver do SQL Server, por exemplo, há quatro páginas de configurações personalizadas.) Depois de você concluir, o novo DSN de sistema aparecerá na lista.

    ![Novo DSN de sistema na lista](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Retorne para o assistente e insira o nome do DSN no campo **Dsn** na página **Escolher uma fonte de dados** ou **Escolher um destino**. Continue para a próxima etapa do assistente.

## <a name="option-2---provide-a-connection-string"></a><a name="odbc_connstring"></a> Opção 2 – fornecer uma cadeia de conexão
Se você quiser fornecer suas informações de conexão com uma cadeia de conexão, o restante deste tópico lhe ajudará a obter a cadeia de conexão necessária.

Este exemplo usará a cadeia de conexão a seguir, que se conecta ao Microsoft SQL Server. O exemplo de banco de dados usado é **WideWorldImporters** e estamos nos conectando ao SQL Server no computador local.

```console
Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
```

Insira a cadeia de conexão no campo **ConnectionString** na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Depois de inserir a cadeia de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

Esta é a tela que você vê depois de inserir a cadeia de conexão.

![Conectar-se ao SQL com o ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> As opções de conexão para o driver ODBC serão as mesmas independentemente de você estar configurando sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

## <a name="get-the-connection-string-online"></a>Obter a cadeia de conexão online
Para localizar as cadeias de conexão para o driver ODBC online, consulte [The Connection Strings Reference](https://www.connectionstrings.com/) (A Referência de Cadeias de Conexão). Esse site de terceiros contém cadeias de conexão de exemplo e mais informações sobre provedores de dados e as informações de conexão exigidas por elas.

## <a name="get-the-connection-string-with-an-app"></a>Obter a cadeia de conexão com um aplicativo
Para compilar e testar a cadeia de conexão para o driver ODBC no seu próprio computador, você pode usar o miniaplicativo **Administrador de Fonte de Dados ODBC** no Painel de Controle. Crie um DSN de arquivo para a conexão e, em seguida, copie as configurações do DSN de arquivo para montar a cadeia de conexão. Isso requer várias etapas, mas ajuda a verificar se você tem uma cadeia de conexão válida.

1.  Pesquise pelo miniaplicativo **fontes de dados ODBC (64 bits)** ou navegue até ele no Menu Iniciar ou Painel de Controle. Se você só tem um driver de 32 bits ou deve usar um driver de 32 bits, em vez disso, pesquise pelas **Fontes de Dados ODBC (32 bits)** ou navegue até elas.
2.  Inicie o miniaplicativo. A janela **Administrador de Fonte de Dados ODBC** se abre.
3.  Agora vá para a guia **DSN de Arquivo** do miniaplicativo. Clique em **Adicionar**.

    Para este exemplo, crie um DSN de arquivo em vez de um DSN de usuário ou DSN de sistema, porque o DSN de arquivo salva os pares nome-valor no formato específico necessário para a cadeia de conexão.

    ![Adicionar um novo DSN de arquivo ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  Na caixa de diálogo **Criar nova fonte de dados**, selecione o driver na lista e, em seguida, clique em **Avançar**. Este exemplo vai criar um DSN que contém os argumentos de cadeia de conexão necessários para conexão com o Microsoft SQL Server.

    ![Criar uma nova fonte de dados ODBC](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Selecione um local e digite um nome para o novo DSN de arquivo e, em seguida, clique em **Avançar**. Lembre-se do local em que você salvar o arquivo para que você possa encontrá-lo e abri-lo em uma etapa posterior.

    ![Salvar o novo DSN de arquivo](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Examine o resumo de suas seleções e, em seguida, clique em **Concluir**.

7.  Depois de clicar em **Concluir**, o driver que você selecionou exibe uma ou mais telas proprietárias para coletar as informações de que ele precisa para se conectar. Geralmente essas informações incluem servidor, informações de logon e banco de dados para fontes de dados com base em servidor ou então arquivo, formato e versão para fontes de dados com base em arquivo.

8. Depois de configurar sua fonte de dados e clicar em **Concluir**, normalmente você vê um resumo das suas seleções e tem a oportunidade de testá-las.

    ![Testar o novo DSN de arquivo](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Depois de testar sua fonte de dados e fechar as caixas de diálogo, localize o DSN de arquivo no local em que ele foi salvo no sistema de arquivos. Se você não alterou a extensão de arquivo, a extensão padrão é .DSN.

10. Abra o arquivo salvo com o Bloco de Notas ou outro editor de texto. Aqui está o conteúdo do nosso exemplo do SQL Server.

    ```console
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. Copie e cole os valores necessários em uma cadeia de conexão na qual os pares nome-valor são separados por ponto e vírgula.

    Depois que você agrupa os valores necessários do DSN de arquivo de exemplo, você tem a cadeia de conexão a seguir.
    
    ```console
    DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
    ```

    Normalmente, você não precisa de todas as configurações em um DSN criado pelo Administrador de Fonte de Dados do ODBC para criar uma cadeia de conexão que funcione.  
    -   Você sempre precisa especificar o driver ODBC.
    -   Para uma fonte de dados com base em servidor como o SQL Server, você normalmente precisa de servidor, banco de dados e informações de logon. No DSN de exemplo, você não precisa de TrustServerCertificate, WSID nem APP.
    -   Para uma fonte de dados com base em arquivo, você precisa de pelo menos nome e local do arquivo.
    
12. Cole esta cadeia de conexão no campo **ConnectionString** na página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do assistente. O assistente analisa a cadeia de caracteres e você está pronto para continuar!

    ![Conectar-se ao SQL com o ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


