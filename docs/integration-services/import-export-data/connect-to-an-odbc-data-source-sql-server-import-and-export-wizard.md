---
title: "Conectar a uma fonte de dados ODBC (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 0e3ffe2ff1695de69be7149f4be7b42f57b0e991
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados ODBC (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **ODBC** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server.

Você precisará baixar o driver ODBC, você precisa da Microsoft ou de terceiros.

Você também pode ter que pesquisar as informações de conexão necessárias que você precisa fornecer. Este site de terceiros - [a referência de cadeias de caracteres de Conexão](https://www.connectionstrings.com/) -contém cadeias de caracteres de conexão de exemplo e obter mais informações sobre provedores de dados e as informações de conexão que eles exigem.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Verifique se o driver que você deseja está instalado
1.  Pesquise ou navegue até o **fontes de dados ODBC (64 bits)** miniaplicativo do painel de controle. Se tiver apenas um driver de 32 bits, ou você sabe que você precisa usar um driver de 32 bits, pesquise ou navegue até **fontes de dados ODBC (32 bits)** em vez disso.
2.  Inicie o miniaplicativo. O **administrador de fonte de dados ODBC** janela será aberta.
3.  Sobre o **Drivers** guia, você pode encontrar uma lista de todos os drivers ODBC instalados no seu computador. (Os nomes de alguns dos drivers podem ser listados em vários idiomas.)

    Aqui está um exemplo da lista de drivers de 64 bits instalados.

    ![Drivers ODBC de 64 bits instalados](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Se você souber que o driver instalado e você não vê-lo no miniaplicativo de 64 bits, procure no miniaplicativo de 32 bits. Isso também indica se é necessário executar o SQL Server Import e Assistente para exportação de 64 bits ou 32 bits.
>
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.
    
## <a name="step-1---select-the-data-source"></a>Etapa 1: selecione a fonte de dados
Os drivers ODBC instalados no seu computador não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **.NET Framework Data Provider para ODBC** como a fonte de dados no **escolher uma fonte de dados** ou **escolha um destino** página do assistente. Este provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o provedor de dados .NET Framework para ODBC.

![Conectar ao SQL com ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Etapa 2: fornecer informações de conexão
A próxima etapa é fornecer as informações de conexão para o driver ODBC e sua fonte de dados. Você tem duas opções.
1.  Fornecer um **DSN** (nome de fonte de dados) que já exista ou que você criar com o **administrador de fonte de dados ODBC** miniaplicativo do painel de controle. Um DSN é a coleção salva de configurações necessárias para se conectar a uma fonte de dados ODBC.

    Se você já souber o nome DSN ou sabe como criar um novo DSN agora, você pode ignorar o restante desta página. Digite o nome DSN no **Dsn** campo o **escolher uma fonte de dados** ou **escolha um destino** página e continue para a próxima etapa do assistente.

    [Forneça um DSN](#odbc_dsn)
    
2.  Forneça um **cadeia de caracteres de conexão**, que você pode pesquisar online, ou criar e testar em seu computador com o **administrador de fonte de dados ODBC** miniaplicativo.

    Se você já tem a cadeia de caracteres de conexão ou como criá-lo, você pode ignorar o restante desta página. Insira a cadeia de conexão a **ConnectionString** campo o **escolher uma fonte de dados** ou **escolha um destino** página e continue para a próxima etapa do assistente.

    [Forneça uma cadeia de caracteres de conexão](#odbc_connstring)

Se você fornecer uma cadeia de caracteres de conexão, o **escolher uma fonte de dados** ou **escolha um destino** página exibe todas as informações de conexão que o assistente irá usar para se conectar à fonte de dados, como o método de autenticação e nome de servidor e banco de dados. Se você fornecer um DSN, essas informações não estiverem visíveis.

## <a name="odbc_dsn"></a>Opção 1 - fornecer um DSN
Se você quiser fornecer as informações de conexão com um DSN (nome de fonte de dados), use o **administrador de fonte de dados ODBC** miniaplicativo para localizar o nome de fonte de dados existente ou criar um novo DSN.
1.  Pesquise ou navegue até o **fontes de dados ODBC (64 bits)** miniaplicativo do painel de controle. Se você só tiver um driver de 32 bits ou deve usar um driver de 32 bits, pesquise ou navegue até **fontes de dados ODBC (32 bits)** em vez disso.
2.  Inicie o miniaplicativo. O **administrador de fonte de dados ODBC** janela será aberta. O miniaplicativo é semelhante ao seguinte.

    ![Miniaplicativo de painel de controle do administrador de ODBC](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Se você quiser **usar um DSN existente** para sua fonte de dados, você pode usar qualquer DSN que você vê no **DSN do usuário**, **DSN de sistema**, ou **DSN de arquivo** guia. Verifique o nome, em seguida, volte para o assistente e inseri-lo no **Dsn** campo o **escolher uma fonte de dados** ou **escolha um destino** página. Ignore o restante desta página e continue para a próxima etapa do assistente.
4.  Se você quiser **criar um novo DSN**, decida se você deseja que ele fique visível apenas para você (DSN do usuário), visível para todos os usuários do computador Windows incluindo serviços (DSN do sistema) ou salvos em um arquivo (DSN de arquivo). Este exemplo cria um novo DSN de sistema.
5. Sobre o **DSN de sistema** , clique em **adicionar**.

    ![Adicionar um novo sistema ODBC DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  No **criar uma nova fonte de dados** caixa de diálogo, selecione o driver de fonte de dados e clique em **concluir**.

    ![Selecione o driver para o novo sistema DSN](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. O driver agora exibe um ou mais telas específicos de driver em que você insira as informações necessárias para se conectar à fonte de dados. (Para o driver do SQL Server, por exemplo, há quatro páginas de configurações personalizadas.) Depois de concluir, o novo sistema DSN aparece na lista.

    ![Novo DSN de sistema na lista](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Volte para o assistente e digite o nome DSN no **Dsn** campo o **escolher uma fonte de dados** ou **escolha um destino** página. Continue para a próxima etapa do assistente.

## <a name="odbc_connstring"></a>Opção 2 - fornecer uma cadeia de caracteres de conexão
Se você quiser fornecer suas informações de conexão com uma cadeia de caracteres de conexão, o restante deste tópico o ajuda a obter a cadeia de conexão que é necessário.

Este exemplo usará a cadeia de conexão a seguir, que se conecta ao Microsoft SQL Server.

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

Insira a cadeia de conexão do **ConnectionString** campo o **escolher uma fonte de dados** ou **escolha um destino** página. Depois de inserir a cadeia de caracteres de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

Esta é a tela que você vê depois de inserir a cadeia de caracteres de conexão.

![Conectar ao SQL com ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> As opções de conexão para um driver ODBC são os mesmos se você estiver configurando a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

## <a name="get-the-connection-string-online"></a>Obter a cadeia de conexão online
Para localizar as cadeias de caracteres de conexão para o ODBC driver on-line, consulte [a referência de cadeias de caracteres de Conexão](https://www.connectionstrings.com/). Este site de terceiros contém cadeias de caracteres de conexão de exemplo e obter mais informações sobre provedores de dados e as informações de conexão que eles exigem.

## <a name="get-the-connection-string-with-an-app"></a>Obter a cadeia de conexão com um aplicativo
Para compilar e testar a cadeia de caracteres de conexão para o driver ODBC no seu próprio computador, você pode usar o **administrador de fonte de dados ODBC** miniaplicativo do painel de controle. Criar um DSN de arquivo para a conexão, em seguida, copiar configurações sem o DSN de arquivo para montar a cadeia de conexão. Isso requer várias etapas, mas ajuda a certificar-se de que você tem uma cadeia de caracteres de conexão válido.

1.  Pesquise ou navegue até o **fontes de dados ODBC (64 bits)** miniaplicativo do painel de controle. Se você só tiver um driver de 32 bits ou deve usar um driver de 32 bits, pesquise ou navegue até **fontes de dados ODBC (32 bits)** em vez disso.
2.  Inicie o miniaplicativo. O **administrador de fonte de dados ODBC** janela será aberta.
3.  Agora vá para o **DSN de arquivo** guia do miniaplicativo. Clique em **Adicionar**.

    Para este exemplo, crie um DSN de arquivo em vez de um DSN de usuário ou DSN de sistema, como o DSN de arquivo salva os pares nome-valor no formato específico necessário para a cadeia de caracteres de conexão.

    ![Adicionar um novo arquivo ODBC DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  No **criar nova fonte de dados** caixa de diálogo, selecione o driver na lista e, em seguida, clique em **próximo**. Este exemplo vai criar um DSN que contém os argumentos de cadeia de caracteres de conexão que é necessário para se conectar ao Microsoft SQL Server.

    ![Criar nova fonte de dados ODBC](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Selecione um local e digite um nome para o novo DSN de arquivo e, em seguida, clique em **próximo**. Lembre-se de que você salvar o arquivo para que você pode encontrá-lo e abri-lo em uma etapa posterior.

    ![Salvar o novo DSN de arquivo](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Revise o resumo de suas seleções e, em seguida, clique em **concluir**.

7.  Depois de clicar em **concluir**, o driver que você selecionou exibe um ou mais telas proprietárias para coletar as informações necessárias para se conectar. Geralmente essas informações incluem servidor, informações de logon e o banco de dados para fontes de dados com base em servidor e o arquivo, o formato e versão para fontes de dados com base em arquivo.

8. Depois de configurar sua fonte de dados e clique em **concluir**, normalmente você ver um resumo das suas seleções e terá a oportunidade de testá-las.

    ![DSN de arquivo novo teste](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Depois de testar sua fonte de dados e feche as caixas de diálogo, localize o DSN de arquivo onde ele foi salvo no sistema de arquivos. Se você não alterar a extensão de arquivo, a extensão padrão é. DSN.

10. Abra o arquivo salvo com o bloco de notas ou outro editor de texto. Aqui está o conteúdo do nosso exemplo do SQL Server.

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=Microsoft® Windows® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. Copie e cole os valores necessários em uma cadeia de caracteres de conexão na qual os pares nome-valor são separados por ponto e vírgula.

    Depois que você agrupa os valores necessários do DSN de arquivo de exemplo, você tem a seguinte cadeia de conexão.
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    Todas as configurações em um DSN criado pelo administrador de fonte de dados do ODBC para criar uma cadeia de conexão que funcione normalmente não é necessário.  
    -   Você sempre precisa especificar o driver ODBC.
    -   Para uma fonte de dados com base em servidor como o SQL Server, você normalmente precisa de servidor, banco de dados e informações de logon. No exemplo de DSN, que exige TrustServerCertificate, WSID ou aplicativo.
    -   Para uma fonte de dados com base em arquivo, você precisa de pelo menos arquivo nome e local.
    
12. Cole essa cadeia de caracteres de conexão para o **ConnectionString** campo o **escolher uma fonte de dados** ou **escolha um destino** página do assistente. O assistente analisa a cadeia de caracteres e você está pronto para continuar!

    ![Conectar ao SQL com ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



