---
title: Conectar-se a uma fonte de dados do Access (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 67a361446c69425f6b05bef913ded568a7dcfd75
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296300"
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do Access (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tópico mostra como se conectar a uma fonte de dados do **Microsoft Access** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server.

A captura de tela a seguir mostra uma conexão de exemplo a um banco de dados do Microsoft Access. Neste exemplo, você não precisa inserir um nome de usuário e senha, porque o banco de dados de destino não usa um arquivo de informações do grupo de trabalho.

![Conectar-se ao Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Opções a serem especificadas

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o Access for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

**Fonte de dados**  
A lista de provedores de dados pode conter várias entradas para o Microsoft Access. Selecione a versão instalada mais recente ou a versão que corresponde à versão do Access que criou o arquivo de banco de dados.

|Fonte de dados|Versão do Office|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Mecanismo de Banco de Dados do Microsoft Access)|Office 2010 e Office 2007|
|Microsoft Access (Mecanismo de Banco de Dados do Microsoft Jet)|Versões do Office anteriores ao Office 2007|

> [!IMPORTANT]
> Talvez seja necessário baixar e instalar arquivos adicionais para se conectar a bancos de dados do Access. Consulte [Obter os arquivos necessários para se conectar ao Access](#officeDownloads) nesta página para obter mais informações.

 **Nome do arquivo**  
Especifique o nome do arquivo e o caminho completo para o arquivo do Access. Por exemplo, **C:\\MyData.mdb** para um arquivo no computador local ou **\\\\Sales\\Database\\Northwind.mdb** para um arquivo em um compartilhamento de rede. Se preferir, clique em **Procurar**. 

> [!NOTE]
> Se você clicar em **Procurar** para localizar o arquivo de acesso, a caixa de diálogo **Abrir** filtra para arquivos com o formato e a extensão de nome de arquivo .MDB mais antigos por padrão. No entanto, o provedor de dados também pode abrir arquivos com o formato e a extensão de nome de arquivo .ACCDB mais recentes.
  
 **Procurar**  
 Localize o arquivo de banco de dados usando a caixa de diálogo **Abrir**.  
  
 **Nome de usuário**  
Se um arquivo de informações do grupo de trabalho estiver associado ao banco de dados, forneça um nome de usuário válido.  
  
 **Senha**  
Se um arquivo de informações do grupo de trabalho estiver associado ao banco de dados, forneça a senha do usuário aqui.
 
Se o banco de dados estiver protegido com uma única senha para todos os usuários, consulte [O arquivo de banco de dados está protegido por senha?](#database_password).
  
 **Avançado**  
Especifique as opções avançadas, como a senha do banco de dados ou um arquivo de informações do grupo de trabalho não padrão, usando a caixa de diálogo **Propriedades de Vínculo de Dados**.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Não vejo o Access na lista de fontes de dados
Se você não vê o Access na lista de fontes de dados, você está executando o assistente de 64 bits? Os provedores para o Excel e Access são geralmente de 32 bits e não são visíveis no assistente de 64 bits. Em vez disso, execute o Assistente de 32 bits.

> [!NOTE]
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="officeDownloads"></a>Obter os arquivos necessários para se conectar ao Access  
Talvez seja preciso baixar os componentes de conectividade para as fontes de dados do Microsoft Office, incluindo Excel e Access, se eles ainda não estiverem instalados. Baixe a versão mais recente dos componentes de conectividade para arquivos do Excel e do Access aqui: [Mecanismo de Banco de Dados do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes podem abrir arquivos criados em versões anteriores do Access.

Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos componentes e precisará também certificar-se de executar o pacote no modo de 32 bits.

Se você tem uma assinatura do Office 365, verifique se você baixou o Mecanismo de Banco de Dados do Access 2016 Redistribuível e não o Runtime do Microsoft Access 2016. Quando você executar o instalador, você verá uma mensagem de erro dizendo que você não pode instalar o download lado a lado com componentes do tipo clique para executar do Office. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de Comando e executando o arquivo .EXE baixado com a opção `/quiet`. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> O arquivo de banco de dados está protegido por senha?
Em alguns casos, um banco de dados do Access está protegido por senha, mas não está usando um arquivo de informações do grupo de trabalho. Todos os usuários precisam fornecer a mesma senha, mas não precisam digitar um nome de usuário. Para fornecer uma senha de banco de dados, faça o descrito a seguir.

1.  Na página **Escolher uma fonte de dados** ou **Escolher um destino**, clique no botão **Avançado** para abrir a caixa de diálogo **Propriedades de Vínculo de Dados**.  
2.  Na caixa de diálogo **Propriedades de Vínculo de Dados**, clique em **Todas**.  
3.  Na lista de propriedades e valores, selecione **Jet OLEDB:Senha do Banco de Dados**.   
    
    ![Especificar a senha do Access, tela 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Clique em **Editar Valor** para abrir a caixa de diálogo **Editar Valor da Propriedade**.  
    
    ![Especificar a senha do Access, tela 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  Na caixa de diálogo **Editar Valor da Propriedade**, digite a senha do banco de dados.
6.  Clique em **OK** em cada caixa de diálogo para retornar para a página **Escolher uma fonte de dados** ou **Escolha um destino** do assistente e continuar.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Manter os valores de numeração automática quando você exporta do Access
Para permitir que valores de identidade existentes nos dados de origem sejam inseridos em uma coluna de identidade na tabela de destino, escolha a opção **Habilitar inserção de identidade** na caixa de diálogo **Mapeamentos de Coluna**. Por padrão, a coluna de identidade de destino geralmente não permite inserir valores existentes. Para mostrar a caixa de diálogo **Mapeamentos de Coluna**, selecione **Editar Mapeamentos** quando você chegar à página **Selecionar tabelas de origem e exibições** do assistente. Para ver essas páginas, consulte [Selecionar tabelas de origem e exibições](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) e [Mapeamentos de Coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Se suas chaves primárias existentes estiverem em uma coluna de identidade, uma coluna autonumber ou equivalente, normalmente você precisará selecionar esta opção para manter os valores de chave primária existentes. Caso contrário, a coluna de identidade de destino normalmente atribui novos valores.

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

