---
title: "Conectar a uma fonte de dados do Access (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
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
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 71bb3914e31259bc95a1116c2db03708c0442e8c
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados do Access (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **Microsoft Access** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server.

A captura de tela a seguir mostra uma conexão de exemplo a um banco de dados do Microsoft Access. Neste exemplo, você não precisa inserir um nome de usuário e senha, porque o banco de dados de destino não usa um arquivo de informações do grupo de trabalho.

![Conecte-se para acesso](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Opções para especificar

> [!NOTE]
> As opções de conexão para este provedor de dados são o mesmo se o acesso é a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

**Fonte de dados**  
A lista de provedores de dados pode conter várias entradas para o Microsoft Access. Selecione a versão instalada mais recente ou a versão que corresponde à versão do Access que criou o arquivo de banco de dados.

|Fonte de dados|Versão do Office|
|-------|-------|
|O Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|O Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|O Microsoft Access (mecanismo de banco de dados do Microsoft Access)|Office 2010 e Office 2007|
|O Microsoft Access (mecanismo de banco de dados do Microsoft Jet)|Versões do Office anteriores ao Office 2007|

> [!IMPORTANT]
> Você precisará baixar e instalar arquivos adicionais para se conectar aos bancos de dados do Access. Consulte [obter os arquivos que você precisa se conectar para acessar](#officeDownloads) nesta página para obter mais informações.

 **Nome do arquivo**  
Especifique o caminho e nome de arquivo para o arquivo do Access. Por exemplo, **c:\\MyData.mdb** para um arquivo no computador local, ou  **\\ \\vendas\\banco de dados\\mdb** para um arquivo em um compartilhamento de rede. Se preferir, clique em **Procurar**. 

 >   [!NOTE] 
 > Se você clicar em **procurar** para localizar o arquivo de acesso, o **abrir** filtros de caixa de diálogo para arquivos com o mais antigo. Extensão MDB de formato e o arquivo por padrão. No entanto o provedor de dados também pode abrir arquivos com o mais recente. Extensão de arquivo e de formato ACCDB.
  
 **Procurar**  
 Localize o arquivo de banco de dados usando a caixa de diálogo **Abrir**.  
  
 **Nome de usuário**  
Se um arquivo de informações do grupo de trabalho está associado com o banco de dados, forneça um nome de usuário válido.  
  
 **Senha**  
Se um arquivo de informações do grupo de trabalho está associado com o banco de dados, forneça a senha do usuário aqui.
 
Se o banco de dados estiver protegido com uma única senha para todos os usuários, consulte [é o arquivo de banco de dados protegido por senha?](#database_password).
  
 **Avançado**  
Especifique opções avançadas, como a senha do banco de dados ou um arquivo de informações do grupo de trabalho não padrão, no **propriedades de vínculo de dados** caixa de diálogo.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Não vejo acesso na lista de fontes de dados
Se você não vir o acesso na lista de fontes de dados, você está executando o Assistente de 64 bits? Os provedores para o Excel e Access são geralmente de 32 bits e não são visíveis no Assistente de 64 bits. Execute o Assistente de 32 bits em vez disso.

> [!NOTE]
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="officeDownloads"></a>Obter os arquivos que você precisa se conectar para acessar  
Você precisará baixar os componentes de conectividade para fontes de dados do Microsoft Office, inclusive o Access e o Excel, se eles ainda não estiverem instalados. Baixar a versão mais recente dos componentes de conectividade para acessar e Excel arquivos aqui: [redistribuível de 2016 do mecanismo de banco de dados Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes pode abrir arquivos criados por versões anteriores do Access.

Se o computador tiver uma versão de 32 bits do Office, em seguida, você precisa instalar a versão de 32 bits dos componentes e você também precisa garantir que você execute o pacote no modo de 32 bits.

Se você tiver uma assinatura do Office 365, certifique-se de que você baixe o redistribuível de 2016 do mecanismo de banco de dados de acesso e não o Microsoft Access 2016 Runtime. Quando você executar o instalador, você verá uma mensagem de erro que você não pode instalar a download lado a lado com componentes do Office clique para executar. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de comando e executando o. Arquivo EXE baixado com o `/quiet` alternar. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a>É o arquivo de banco de dados protegido por senha?
Em alguns casos, um banco de dados protegido por senha, mas não está usando um arquivo de informações do grupo de trabalho. Todos os usuários precisam fornecer a mesma senha, mas não terá que digitar um nome de usuário. Para fornecer uma senha de banco de dados, faça o seguinte:

1.  No **escolher uma fonte de dados** ou **escolha um destino** , clique no **avançado** para abrir o **propriedades de vínculo de dados** caixa de diálogo.  
2.  No **propriedades de vínculo de dados** caixa de diálogo, selecione o **todas as** guia.  
3.  Na lista de propriedades e valores, selecione **Jet OLEDB:Database senha**.   
    
    ![Especifique a senha de acesso, a tela 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Clique em **Editar valor** para abrir o **Editar valor da propriedade** caixa de diálogo.  
    
    ![Especifique a senha de acesso, tela de 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  No **Editar valor da propriedade** caixa de diálogo caixa, digite a senha do banco de dados.
6.  Clique em **Okey** em cada caixa de diálogo para retornar para o **escolher uma fonte de dados** ou **escolha um destino** página do assistente e continuar.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Manter os valores de numeração automática quando você exporta do Access
Para permitir que os valores de identidade existentes na fonte de dados a ser inserido em uma coluna de identidade na tabela de destino, escolha o **habilitar inserção de identidade** opção o **mapeamentos de coluna** caixa de diálogo. Por padrão, a coluna de identidade de destino geralmente não permite que você inserir valores existentes. Para mostrar o **mapeamentos de coluna** caixa de diálogo, selecione **editar mapeamentos** quando você atingir o **selecionar tabelas de origem e exibições** página do assistente. Para ver essas páginas, consulte [selecionar tabelas de origem e exibições](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) e [mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Se suas chaves primárias existentes estiverem em uma coluna de identidade, uma coluna autonumber ou equivalente, normalmente você precisará selecionar esta opção para manter os valores de chave primária existentes. Caso contrário, a coluna de identidade de destino normalmente atribui novos valores.

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


