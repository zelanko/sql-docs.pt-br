---
title: Escolher uma fonte de dados (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 18b97b67590bfff4f01e5dff332722a3aba1cf7e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436873"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Escolher uma fonte de dados (Assistente de Importação e Exportação do SQL Server)
  Use a página **escolher uma fonte de dados** para especificar a origem dos dados que você deseja copiar.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Fonte de Dados**  
 Escolha o provedor de dados que corresponde ao formato de armazenamento da origem. Pode haver mais de um provedor disponível para sua fonte de dados. Por exemplo, com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native Client, o .NET Framework Provedor de Dados para SQL Server ou o provedor de OLE DB da Microsoft para SQL Server.  
  
 A propriedade **fonte de dados** tem um número variável de opções, que dependem dos provedores instalados no computador. As tabelas a seguir listam as opções de alguns destinos usados com mais frequência. Para outros provedores, consulte a documentação específica do provedor.  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
 As seções a seguir mostram as opções disponíveis para várias fontes de dados. Nem todas as fontes de dados disponíveis no menu suspenso Fonte de Dados são listadas aqui.  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>Fonte de Dados = SQL Server Native Client e Microsoft OLE DB Provider for SQL Server  
 **Nome do servidor**  
 Digite o nome do servidor que contém os dados ou escolha um servidor da lista.  
  
 **Usar Autenticação do Windows**  
 Especifique se o pacote deve usar a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para fazer login no banco de dados. A Autenticação do Windows é recomendada para obter melhor segurança.  
  
 **Usar autenticação SQL Server**  
 Especifique se o pacote deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer login no banco de dados. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para estabelecer conexão com o banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Backup de banco de dados**  
 Selecione usando a lista de bancos de dados na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Atualizar**  
 Restaure a lista de bancos de dados disponíveis clicando em **Atualizar**.  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>Fonte de Dados = .NET Framework Data Provider for SQL Server  
 Esta página apresenta uma lista alfabética de opções para o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As opções mais importantes estão listadas na tabela a seguir.  
  
 **Fonte de Dados**  
 Digite o nome do servidor que contém os dados ou escolha um servidor da lista.  
  
 **Catálogo Inicial**  
 Digite o nome do banco de dados de origem.  
  
 **Segurança Integrada**  
 Especifique `True` para estabelecer conexão usando a autenticação integrada do Windows (recomendado) ou `False` para estabelecer conexão usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar `False`, deverá inserir uma ID de usuário e uma senha. O valor padrão é `False`.  
  
 **ID de usuário**  
 Especifique um nome de usuário para estabelecer conexão com o banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 As opções adicionais que são listadas ao selecionar esse provedor não são necessárias para estabelecer uma conexão bem-sucedida com o banco de dados de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma descrição dessas opções, consulte a documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Software Development Kit.  
  
### <a name="data-source--microsoft-excel"></a>Fonte de Dados = Microsoft Excel  
  
> [!NOTE]  
>  Selecione **Microsoft Excel** somente se você quiser se conectar a uma fonte de dados que usa o Excel 2003 ou anterior. Para se conectar a uma fonte de dados que usa o Excel 2007, selecione **Microsoft Office 12,0 acesso mecanismo de banco de dados provedor de OLE DB**, clique em **Propriedades**e, em seguida, na guia **tudo** da caixa de diálogo Propriedades do **vínculo de dados** , digite `Excel 12.0` como o valor das **Propriedades estendidas**.  
  
 **Caminho de arquivo do Excel**  
 Especifique o caminho e nome de arquivo da planilha a partir da qual os dados serão importados. Por exemplo, **C:\MyData.xls, \\\Sales\Database\Northwind.xls**. Se preferir, clique em **Procurar**.  
  
 **Procurar**  
 Localize a planilha usando a caixa de diálogo **Abrir**.  
  
 **Versão do Excel**  
 Selecione a versão do Excel em que os dados de origem estão armazenados.  
  
> [!NOTE]  
>  Quando você importa dados de uma origem do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], o assistente usa o componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel Source. Para obter informações sobre algumas considerações sobre uso e problemas conhecidos, consulte [Origem do Excel](../data-flow/excel-source.md).  
  
### <a name="data-source--microsoft-access"></a>Fonte de Dados = Microsoft Access  
  
> [!NOTE]  
>  Selecione **Microsoft Access** somente se você quiser se conectar a um banco de dados que usa o Access 2003 ou anterior. Para se conectar a um banco de dados que usa o Access 2007, selecione **Microsoft Office mecanismo de banco de dados o provedor de OLE DB de acesso 12,0** .  
  
 **Nome do arquivo**  
 Especifique o caminho e nome de arquivo do arquivo de banco de dados a partir do qual os dados serão importados. Por exemplo, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. Se preferir, clique em **Procurar**.  
  
 **Procurar**  
 Localize o arquivo de banco de dados usando a caixa de diálogo **Abrir**.  
  
 **Nome de usuário**  
 Especifique um nome de usuário válido para estabelecer conexão com o banco de dados quando houver um arquivo de informações do grupo de trabalho associado ao banco de dados.  
  
 **Senha**  
 Forneça a senha do usuário para estabelecer conexão quando o arquivo de informações do grupo de trabalho estiver associado ao banco de dados. No entanto, se o banco de dados estiver protegido com uma única senha para todos os usuários, você deverá fornecer esse valor na caixa de diálogo **Propriedades do vínculo de dados** , que é acessada clicando em **avançado**.  
  
 **Avançado**  
 Talvez você queira especificar opções avançadas, como a senha do banco de dados ou um arquivo de informações do grupo de trabalho não padrão, usando a caixa de diálogo **Propriedades do vínculo de dados** . Para obter mais informações sobre as propriedades do provedor de OLE DB, pesquise na seção de acesso a dados da [biblioteca MSDN](https://go.microsoft.com/fwlink/?linkid=62553).  
  
### <a name="data-source--flat-file-source"></a>Fonte de Dados = Fonte de Arquivos Simples  
 Consulte os tópicos a seguir para obter informações sobre as opções para uma fonte de dados de arquivos simples.  
  
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
  
