---
title: Power Pivot Management Dashboard and Usage Data | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f53c8835da14fc3ee41eb9598303f80c062a0e82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208098"
---
# <a name="power-pivot-management-dashboard-and-usage-data"></a>Painel de Gerenciamento Power Pivot e dados de uso
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] é uma coleção de Web parts e relatórios predefinidos na Administração Central do SharePoint que ajuda a administrar uma implantação do SQL Server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint. O Painel de Gerenciamento fornece informações sobre a integridade do servidor, a atividade da pasta de trabalho e a atualização de dados. O painel usa dados da coleta de dados de uso do SharePoint.  
  
  
##  <a name="prereq"></a> Pré-requisitos  
 Você deve ser um administrador de serviços para abrir o Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para um aplicativo do serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que você gerencia.  
  
##  <a name="items"></a> Visão geral das seções do Painel  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] contém as Web parts e relatórios inseridos que fazem busca detalhada em categorias de informações específicas. A lista a seguir descreve cada parte do painel:  
  
|Painel|Descrição|  
|---------------|-----------------|  
|Infraestrutura - Integridade do Serviço|Mostra as tendências de uso de CPU, o consumo de memória e os tempos de resposta de consulta ao longo do tempo, para que você possa avaliar se os recursos do sistema estão se aproximando da capacidade máxima ou estão subutilizados.|  
|Ações|Contém links para outras páginas da Administração Central, incluindo o aplicativo de serviço atual, uma lista dos aplicativos de serviço e o log de uso.|  
|Atividade de Pasta de Trabalho - Gráfico|Relatórios sobre a frequência do acesso a dados. Você pode saber com que frequência as conexões a fontes de dados [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] ocorrem em uma base diária ou semanal.|  
|Atividade de Pasta de Trabalho - Listas|Relatórios sobre a frequência do acesso a dados. Você pode saber com que frequência as conexões a fontes de dados [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] ocorrem em uma base diária ou semanal.|  
|Atualização de Dados - Atividade Recente|Relatórios sobre o status de trabalhos de atualização de dados, inclusive de trabalhos que falharam. Esse relatório fornece uma exibição composta das operações de atualização de dados no nível do aplicativo. O administradores podem ver de um relance o número de trabalhos de atualização de dados definidos para todo o aplicativo do serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|Atualização de Dados - Falhas Recentes|Lista as pastas de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que não concluíram a atualização de dados com êxito.|  
|Relatórios|Contém links para relatórios que você pode abrir no Excel.|  
  
##  <a name="open"></a> Abrir o Painel de Gerenciamento Power Pivot  
 O painel mostra as informações de um aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] por vez. Você pode abrir o painel de gerenciamento em dois lugares diferentes.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>Abra o painel em Configurações Gerais do Aplicativo  
  
1.  Na Administração Central, no grupo **Configurações Gerais do Aplicativo**, clique em **Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** .  
  
2.  Na página principal, selecione o aplicativo do serviço Power Pivot para o qual você deseja exibir dados de operações.  
  
### <a name="open-the-dashboard-from-a-power-pivot-service-application"></a>Abra o painel em um aplicativo de serviço Power Pivot  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . O Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] exibe dados operacionais do aplicativo de serviço atual.  
  
### <a name="change-the-current-service-application"></a>Altere o aplicativo de serviço atual.  
 Para alterar o aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] atual no painel de gerenciamento:  
  
1.  Na parte superior a [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] painel de gerenciamento, anote o nome do aplicativo de serviço atual, por exemplo **padrão [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] aplicativo de serviço**.  
  
2.  No painel **Ações** , clique em **Listar aplicativos de serviço**.  
  
3.  Clique no nome do aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] cujos relatórios do painel de gerenciamento você deseja ver.  
  
##  <a name="sourcedata"></a> Fontes de dados em painéis  
 Os painéis, os relatórios e as Web parts mostram dados de um modelo de dados interno que recebe dados do sistema e dos bancos de dados de aplicativo do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . O modelo de dados interno é inserido em uma pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] hospedada no site da Administração Central. A estrutura do modelo de dados é fixa. Embora você possa usar a pasta de trabalho PowerPivot como fonte de dados para criar novos relatórios, não modifique a estrutura de modo a fragmentar os relatórios predefinidos que a utilizam.  
  
 Para obter mais informações sobre como os dados são coletados, consulte:  
  
-   [Coleta de dados de uso do PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
-   [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 Para capturar dados sobre o sistema de servidor do Power Pivot, verifique se as mensagens de eventos, o histórico de atualização de dados e outro histórico de uso estão habilitados para cada aplicativo de serviço Power Pivot. Os dados de servidor e de uso coletados durante as operações normais do servidor são os dados de origem resultantes no modelo de dados interno. **Observação:** Se você desativar eventos ou o histórico de uso, os relatórios compostos serão ser incompletos ou incorretos.  
  
##  <a name="edit"></a> Editar o Painel do Power Pivot  
 Se você tiver experiência em desenvolvimento ou personalização de painéis, poderá editar o painel para incluir novas Web parts. Você também poderá editar as propriedades das Web parts incluídas no painel.  
  
##  <a name="reports"></a> Criar relatórios personalizados para o Painel de Gerenciamento do Power Pivot  
 Para fins de emissão de relatórios, os dados e o histórico de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] são mantidos em uma pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] interna que é criada e configurada junto com o painel de controle. Se os relatórios padrão não fornecerem as informações necessárias, você poderá criar relatórios personalizados no Excel com base na pasta de trabalho. A pasta de trabalho e todos os relatórios personalizados criados serão preservados se você atualizar ou desinstalar os arquivos de solução [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] posteriormente. A pasta de trabalho e os relatórios ficam armazenados na biblioteca de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] no site da Administração Central. Por padrão, essa biblioteca não fica visível, mas você pode exibi-la usando a ação Exibir Todo o Conteúdo do Site em Ações do Site.  
  
 Para começar a usar o recurso de relatórios personalizados, o Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] fornece um arquivo Office Data Connection (.odc) para estabelecer a conexão com a pasta de trabalho de origem. Por exemplo, você pode usar o arquivo .odc no Excel para criar relatórios adicionais.  
  
> [!NOTE]  
>  Edite o arquivo para evitar o seguinte erro ao tentar usar o arquivo. odc no Excel: "Falha na inicialização da fonte de dados". O arquivo .odc gerado automaticamente inclui um parâmetro que não é suportado pelo provedor OLE DB do MSOLAP. As instruções a seguir apresentam a solução de contorno para excluir os parâmetros.  
  
 Você deve ser um administrador de farm ou de serviços para compilar relatórios com base na pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] na Administração Central.  
  
1.  Abra o Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
2.  Role até a seção **Relatórios** na parte inferior da página.  
  
3.  Clique em **Dados de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** .  
  
4.  Salve o arquivo .odc em uma pasta local.  
  
5.  Abra o arquivo .odc em um editor de texto.  
  
6.  No  **\<odc: ConnectionString >** elemento, role até o final da linha e remova **dados inseridos = False**e, em seguida, remover **modo de edição = 0**. Se o último caractere da cadeia de caracteres for um ponto-e-vírgula, exclua-o agora.  
  
7.  Salve o arquivo. As etapas restantes dependem da versão do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e do Excel que você está usando.  
  
8.  1.  Inicie o Excel 2013  
  
    2.  Na faixa de opções **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** , clique em **Gerenciar**.  
  
    3.  Clique em **Obter Dados Externos** e clique em **Conexões existentes**.  
  
    4.  Clique no arquivo .ODC, caso ele seja exibido. Se o arquivo .ODC não for exibido, clique em **Procurar Mais** e, no caminho do arquivo, especifique o arquivo .odc.  
  
    5.  Clique em **Abrir**  
  
    6.  Clique em **Testar Conexão** para verificar se a conexão é estabelecida com êxito.  
  
    7.  Digite um nome para a conexão e clique em **Avançar**.  
  
    8.  Em especificar consulta MDX, clique em **Design** para abrir o designer de consulta MDX e montar os dados que você deseja trabalhar **se você vir a mensagem de erro** "o nome da propriedade modo de edição não é formatado corretamente.", verifique se você as edições do. Arquivo ODC.  
  
    9. Clique em **OK** e em **Concluir**.  
  
    10. Crie os relatórios de Tabela Dinâmica ou Gráfico Dinâmico para visualizar os dados no Excel.  
  
9. 1.  Inicie o Excel 2010.  
  
    2.  Na faixa de opções [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)], clique em **Inicializar Janela [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** .  
  
    3.  Na faixa de opções Design na janela do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , clique em **Conexões Existentes**.  
  
    4.  Clique em **Procurar mais**.  
  
    5.  No caminho do arquivo, especifique o arquivo .odc.  
  
    6.  Clique em **Abrir**. O Assistente de Importação de Tabelas é iniciado, usando a cadeia de conexão com a pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que contém os dados de uso.  
  
    7.  Clique em **Testar a conexão** para verificar se você tem acesso.  
  
    8.  Digite um nome intuitivo para a conexão e, em seguida, clique em **Avançar**.  
  
    9. Em Especificar Consulta MDX, clique em **Design** para abrir o designer de consulta MDX e montar os dados com os quais deseja trabalhar. Em seguida, crie relatórios de Tabela Dinâmica ou Gráfico Dinâmico para visualizar os dados no Excel.  
  
## <a name="see-also"></a>Consulte também  
 [Atualização de dados do Power Pivot com o SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
