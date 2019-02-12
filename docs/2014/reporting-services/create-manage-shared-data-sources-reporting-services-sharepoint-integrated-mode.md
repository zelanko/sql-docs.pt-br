---
title: Criar e gerenciar fontes de dados compartilhadas (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], shared data sources
- shared data sources [Reporting Services]
ms.assetid: 2d3428e4-a810-4e66-a287-ff18e57fad76
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3253c8c13b950f661ee7ddc7925aac19221d3173
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011177"
---
# <a name="create-and-manage-shared-data-sources-reporting-services-in-sharepoint-integrated-mode"></a>Criar e gerenciar fontes de dados compartilhadas (Reporting Services no modo integrado do SharePoint)
  Ao executar um relatório a partir de uma biblioteca do SharePoint, as informações de conexão podem ser definidas no relatório ou em um arquivo externo vinculado ao relatório. Se as informações de conexão estiverem inseridas no relatório, ele será denominado uma fonte de dados personalizada. Se as informações de conexão estiverem definidas em um arquivo externo, ele será denominado uma fonte de dados compartilhados. O arquivo externo pode ser um arquivo de fonte de dados do servidor de relatório (.rsds) ou um arquivo de conexão de dados do Office (.odc).  
  
 Um arquivo .rsds é semelhante a um arquivo .rds, mas tem um esquema diferente. Para criar um arquivo .rsds, você pode publicar um arquivo .rds do Designer de Relatórios ou do Designer de Modelo em uma biblioteca do SharePoint (um novo arquivo .rsds é criado a partir do arquivo .rds original). Se preferir, você pode criar um novo arquivo em uma biblioteca em um site do SharePoint.  
  
 Após criar ou publicar uma fonte de dados compartilhada, você pode editar propriedades de conexão ou excluir o arquivo caso não seja mais utilizado. Antes de excluir uma fonte de dados compartilhada, descubra se ela é usada por relatórios e modelos de relatório. Para tal exiba itens dependentes que fazem referência à fonte de dados compartilhada.  
  
 Embora a lista de itens dependentes informe se existe referência a uma fonte de dados compartilhada, ela não informa se o item está sendo usado ativamente. Para descobrir se uma fonte de dados compartilhados ou um modelo está sendo usado ativamente, você pode revisar os arquivos de log no servidor de relatórios. Se você não tiver acesso aos arquivos de log ou se os arquivos não contiverem as informações desejadas, você poderá mover o relatório para uma pasta inacessível enquanto descobre seu status real.  
  
### <a name="to-create-a-shared-data-source-rsds-file-sharepoint-2010"></a>Para criar um arquivo .rsds (SharePoint 2010)  
  
1.  Clique na guia **Documentos** na faixa de opções da biblioteca.  
  
2.  No menu **Novo Documento** , clique em **Fonte de Dados de Relatório**  
  
    > [!NOTE]  
    >  Caso você não veja o item **Fonte de Dados de Relatório** no menu, isso significa que o tipo de conteúdo da fonte de dados de relatório não foi habilitado. Para obter mais informações, consulte [Adicionar servidor de tipos de conteúdo relatório em uma biblioteca do &#40;Reporting Services no modo integrado do SharePoint&#41;](../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  Em **Nome**, insira um nome descritivo para o arquivo .rsds.  
  
4.  Em **Tipo de Fonte de Dados**, selecione o tipo de fonte de dados na lista. Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
5.  Em **Cadeia de Conexão**, especifique um ponteiro para a fonte de dados e outras configurações necessárias para estabelecer uma conexão com a fonte de dados externa. O tipo de fonte de dados usado determina a sintaxe da cadeia de caracteres de conexão. Para obter mais informações e exemplos, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
6.  Em **Credenciais**, especifique como o servidor de relatório obtém credenciais para acessar a fonte de dados externa. Credenciais podem ser armazenadas, solicitadas, integradas ou configuradas para processamento autônomo do relatório.  
  
    -   Selecione **Autenticação do Windows (integrada)** se desejar acessar os dados usando as credenciais do usuário que abriu o relatório. Não selecione essa opção se o site ou farm do SharePoint utilizar autenticação de formulários ou se conectar com o servidor de relatório usando uma conta confiável. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se a autenticação Kerberos não estiver habilitada, as credenciais do Windows poderão ser passadas apenas para outro computador. Isso significa que, se a fonte de dados externa estiver em outro computador, exigindo uma conexão adicional, você receberá uma mensagem de erro em vez dos dados esperados.  
  
    -   Selecione **Prompt para credenciais** se quiser que o usuário insira suas credenciais sempre que executar o relatório. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório.  
  
    -   Selecione **Credenciais armazenadas** se quiser acessar os dados usando um único conjunto de credenciais. As credenciais são criptografadas antes de serem armazenadas. Você pode selecionar opções que determinam como as credenciais armazenadas são autenticadas. Selecione Usar como credenciais do Windows se as credenciais armazenadas pertencerem a uma conta de usuário do Windows. Selecione **Definir o contexto de execução para esta conta** se desejar definir o contexto de execução no servidor de banco de dados. No caso de bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , essa opção define a função SETUSER. Para obter mais informações, consulte [SETUSER &#40;Transact-SQL&#41;](/sql/t-sql/statements/setuser-transact-sql).  
  
    -   Selecione **Não são necessárias credenciais** se quiser especificar credenciais na cadeia de conexão ou se quiser executar o relatório usando uma conta de privilégios mínimos configurada no servidor de relatório. Se essa conta não estiver configurada no servidor de relatório, os usuários serão solicitados a fornecer suas credenciais, e as operações agendadas que você definir para o relatório não serão executadas.  
  
7.  Selecione **Habilitar esta fonte de dados** se desejar que a fonte de dados esteja ativa. Se a fonte de dados estiver configurada mas não ativa, os usuários verão uma mensagem de erro quando tentarem usar um relatório com base na fonte de dados.  
  
8.  Clique no botão **Testar Conexão** para validar a configuração da fonte de dados.  
  
    > [!NOTE]  
    >  O botão Testar Conexão não tem suporte para o tipo de fonte de dados XML.  
  
9. Clique em **OK** para salvar e criar a fonte de dados compartilhada.  
  
### <a name="to-view-dependent-items"></a>Para exibir itens dependentes  
  
1.  Abra a biblioteca que contém o arquivo .rsds.  
  
2.  Aponte para a fonte de dados compartilhada.  
  
3.  Clique para exibir uma seta para baixo e selecione **Exibir Itens Dependentes**.  
  
     No caso de modelos de relatórios, a lista de itens dependentes mostra os relatórios criados no Construtor de Relatórios. No caso de fontes de dados compartilhadas, a lista de itens dependentes pode incluir relatórios e modelos de relatório.  
  
### <a name="to-delete-a-shared-data-source-rsds-file"></a>Para excluir um arquivo da fonte de dados compartilhada (.rsds)  
  
1.  Abra a biblioteca que contém o arquivo .rsds.  
  
2.  Aponte para a fonte de dados compartilhada.  
  
3.  Clique para exibir uma seta para baixo e clique em **Excluir**.  
  
 Se, por engano, você excluir uma fonte de dados compartilhada que pretendia manter, crie uma nova fonte de dados que contenha as mesmas informações de conexão. Depois de recriar a fonte de dados compartilhada, você deve abrir cada relatório e cada modelo que usava essa fonte de dados e selecionar a fonte de dados compartilhada. O novo item da fonte de dados compartilhada pode ter nome, credenciais ou sintaxe de cadeia de caracteres de conexão diferentes daquele que foi excluído. Desde que a conexão leve à mesma fonte de dados, as propriedades de conexão podem variar em relação aos valores originais.  
  
 Tenha cuidado ao excluir um modelo de relatório. Se você excluir um modelo, não será mais possível abrir e modificar relatórios baseados nesse modelo no Construtor de Relatórios. Se você excluir por engano um modelo usado por relatórios existentes, será preciso gerar novamente o modelo, recriar e salvar os relatórios que usam o modelo e especificar novamente a segurança de todos os itens do modelo que deseje usar. Você não pode simplesmente gerar o modelo de novo e, em seguida, anexá-lo a um relatório existente.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
