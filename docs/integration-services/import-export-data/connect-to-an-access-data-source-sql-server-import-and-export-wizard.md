---
title: "Conectar a uma fonte de dados do Access (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2a5deb6e6ec95e6f6707abe9ad85374b2334e05
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

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
> Você precisará baixar e instalar arquivos adicionais para conectar-se para a versão de acesso que você selecionar. Consulte [obter os arquivos que você precisa se conectar para acessar](#officeDownloads) nesta página para obter mais informações.

Se você tiver um problema quando você especificar uma versão, tente especificar uma versão diferente, até mesmo uma versão anterior. Por exemplo, você pode não ser capaz de instalar os provedores de dados do Office 2016, porque você tem uma assinatura do Microsoft Office 365. Você só pode instalar os provedores de dados para acesso 2016 e Excel 2016 com uma versão de área de trabalho do Microsoft Office. Nesse caso, você pode especificar o Access 2013 em vez de acesso de 2016. As duas versões do provedor são funcionalmente equivalentes. Essa limitação de tempo de execução do Office 2016 é mencionada na [esta postagem de blog](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

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
  
## <a name="officeDownloads"></a>Obter os arquivos que você precisa se conectar para acessar  
Você precisará baixar os componentes de conectividade para fontes de dados do Microsoft Office, incluindo o Excel e Access, se eles ainda não estiverem instalados.

As versões mais recentes dos componentes podem abrir arquivos criados em versões anteriores dos programas. Em muitos casos, as versões anteriores dos componentes também podem abrir arquivos criados por versões mais recentes dos programas. Por exemplo, se você não pode instalar os componentes do Office 2016, use os componentes do Office 2013. As duas versões do provedor são funcionalmente equivalentes. Essa limitação de tempo de execução do Office 2016 é mencionada na [esta postagem de blog](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

Se o computador tem uma versão de 32 bits do Office, isso é normal, mesmo em computadores de 64 bits, você precisa instalar a versão de 32 bits dos componentes. Você também precisa garantir que você execute o Assistente de 32 bits ou executa o pacote de atualização do SQL Server Integration Services que o assistente cria no modo de 32 bits.

|Versão do Microsoft Office|Download|  
|------------------------------|--------------|  
|2016|[Tempo de execução do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Tempo de execução do Microsoft Access 2013](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Tempo de execução do Microsoft Access 2010](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System Driver: componentes de conectividade de dados](https://www.microsoft.com/download/details.aspx?id=23734)|    

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


