---
title: PowerPivot Management Dashboard and Usage Data | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ece3d8a1e9a66ecc6ad05508c975e617c523a9c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071117"
---
# <a name="powerpivot-management-dashboard-and-usage-data"></a>Painel de Gerenciamento PowerPivot e dados de uso
  O Painel de Gerenciamento PowerPivot é uma coleção de web parts e relatórios predefinidos na Administração Central do SharePoint que ajuda a administrar uma implantação do SQL Server PowerPivot para SharePoint. O Painel de Gerenciamento fornece informações sobre a integridade do servidor, a atividade da pasta de trabalho e a atualização de dados. O painel usa dados da coleta de dados de uso do SharePoint.  
  
 [Pré-requisitos](#prereq)  
  
 [Visão geral das seções do painel](#items)  
  
 [Painel de gerenciamento PowerPivot aberto](#open)  
  
 [Fonte de dados em painéis](#sourcedata)  
  
 [Editar o painel do PowerPivot](#edit)  
  
 [Criar relatórios personalizados para o painel de gerenciamento do PowerPivot](#reports)  
  
##  <a name="prereq"></a> Pré-requisitos  
 Você deve ser um administrador de serviço para abrir o Painel de Gerenciamento PowerPivot para um aplicativo do serviço PowerPivot que você gerencia.  
  
##  <a name="items"></a> Visão geral das seções do Painel  
 O Painel de Gerenciamento PowerPivot contém as Web parts e relatórios inseridos que fazem busca detalhada em categorias de informações específicas. A lista a seguir descreve cada parte do painel:  
  
|Painel|Descrição|  
|---------------|-----------------|  
|Infraestrutura - Integridade do Serviço|Mostra as tendências de uso de CPU, o consumo de memória e os tempos de resposta de consulta ao longo do tempo, para que você possa avaliar se os recursos do sistema estão se aproximando da capacidade máxima ou estão subutilizados.|  
|Ações|Contém links para outras páginas da Administração Central, incluindo o aplicativo de serviço atual, uma lista dos aplicativos de serviço e o log de uso.|  
|Atividade de Pasta de Trabalho - Gráfico|Relatórios sobre a frequência do acesso a dados. Você pode saber com que frequência as conexões a fontes de dados PowerPivot ocorrem em uma base diária ou semanal.|  
|Atividade de Pasta de Trabalho - Listas|Relatórios sobre a frequência do acesso a dados. Você pode saber com que frequência as conexões a fontes de dados PowerPivot ocorrem em uma base diária ou semanal.|  
|Atualização de Dados - Atividade Recente|Relatórios sobre o status de trabalhos de atualização de dados, inclusive de trabalhos que falharam. Esse relatório fornece uma exibição composta das operações de atualização de dados no nível do aplicativo. O administradores podem ver de um relance o número de trabalhos de atualização de dados definidos para todo o aplicativo do serviço PowerPivot.|  
|Atualização de Dados - Falhas Recentes|Lista as pastas de trabalho PowerPivot que não concluíram a atualização de dados com êxito.|  
|Relatórios|Contém links para relatórios que você pode abrir no Excel.|  
  
##  <a name="open"></a> Painel de gerenciamento PowerPivot aberto  
 O painel mostra as informações de um aplicativo de serviço PowerPivot por vez. Você pode abrir o painel de gerenciamento em dois lugares diferentes.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>Abra o painel em Configurações Gerais do Aplicativo  
  
1.  Na Administração Central, no grupo **Configurações Gerais do Aplicativo** , clique em **Painel de Gerenciamento PowerPivot**.  
  
2.  Na página principal, selecione o aplicativo do serviço PowerPivot para o qual você deseja exibir dados de operações.  
  
### <a name="open-the-dashboard-from-a-powerpivot-service-application"></a>Abra a página em um aplicativo de serviço PowerPivot  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de serviço PowerPivot. O Painel de Gerenciamento PowerPivot exibe dados operacionais do aplicativo de serviço atual.  
  
### <a name="change-the-current-service-application"></a>Altere o aplicativo de serviço atual.  
 Para alterar o aplicativo de serviço PowerPivot atual no painel de gerenciamento:  
  
1.  Na parte superior do painel de gerenciamento PowerPivot, observe o nome do aplicativo de serviço atual, por exemplo **aplicativo de serviço PowerPivot padrão**.  
  
2.  No painel **Ações** , clique em **Listar aplicativos de serviço**.  
  
3.  Clique no nome do aplicativo de serviço PowerPivot cujos relatórios do painel de gerenciamento você deseja ver.  
  
##  <a name="sourcedata"></a> Fontes de dados em painéis  
 Os painéis, os relatórios e as web parts mostram dados de um modelo de dados interno que recebe dados do sistema e dos bancos de dados de aplicativo do PowerPivot. O modelo de dados interno é inserido em uma pasta de trabalho PowerPivot hospedada no site da Administração Central. A estrutura do modelo de dados é fixa. Embora você possa usar a pasta de trabalho PowerPivot como fonte de dados para criar novos relatórios, não modifique a estrutura de modo a fragmentar os relatórios predefinidos que a utilizam.  
  
 Para obter mais informações sobre como os dados são coletados, consulte:  
  
-   [Coleta de dados de uso do PowerPivot](power-pivot-usage-data-collection.md)  
  
-   [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 Para capturar dados sobre o sistema de servidor do PowerPivot, verifique se as mensagens de eventos, o histórico de atualização de dados e outro histórico de uso estão habilitados para cada aplicativo de serviço PowerPivot. Os dados de servidor e de uso coletados durante as operações normais do servidor são os dados de origem resultantes no modelo de dados interno. **Observação:** Se você desativar eventos ou o histórico de uso, os relatórios compostos serão ser incompletos ou incorretos.  
  
##  <a name="edit"></a> Editar o painel do PowerPivot  
 Se você tiver experiência em desenvolvimento ou personalização de painéis, poderá editar o painel para incluir novas Web parts. Você também poderá editar as propriedades das Web parts incluídas no painel.  
  
##  <a name="reports"></a> Criar relatórios personalizados para o painel de gerenciamento do PowerPivot  
 Para fins de emissão de relatórios, os dados e o histórico de uso do PowerPivot são mantidos em uma pasta de trabalho interna PowerPivot que é criada e configurada junto com o painel de controle. Se os relatórios padrão não fornecerem as informações necessárias, você poderá criar relatórios personalizados no Excel com base na pasta de trabalho. A pasta de trabalho e todos os relatórios personalizados criados serão preservados se você atualizar ou desinstalar os arquivos de solução PowerPivot posteriormente. A pasta de trabalho e os relatórios ficam armazenados na biblioteca de Gerenciamento do PowerPivot no site da Administração Central. Por padrão, essa biblioteca não fica visível, mas você pode exibi-la usando a ação Exibir Todo o Conteúdo do Site em Ações do Site.  
  
 Para começar a usar o recurso de relatórios personalizados, o Painel de Gerenciamento PowerPivot fornece um arquivo Office Data Connection (.odc) para estabelecer a conexão com a pasta de trabalho de origem. Por exemplo, você pode usar o arquivo .odc no Excel para criar relatórios adicionais.  
  
> [!NOTE]  
>  Edite o arquivo para evitar o seguinte erro ao tentar usar o arquivo. odc no Excel: "Falha na inicialização da fonte de dados". O arquivo .odc gerado automaticamente inclui um parâmetro que não é suportado pelo provedor OLE DB do MSOLAP. As instruções a seguir apresentam a solução de contorno para excluir os parâmetros.  
  
 Você deve ser um administrador de farm ou de serviço para criar relatórios com base na pasta de trabalho PowerPivot na Administração Central.  
  
1.  Abrir o Painel de Gerenciamento PowerPivot.  
  
2.  Role até a seção **Relatórios** na parte inferior da página.  
  
3.  Clique em **Dados de Gerenciamento do PowerPivot**.  
  
4.  Salve o arquivo .odc em uma pasta local.  
  
5.  Abra o arquivo .odc em um editor de texto.  
  
6.  No elemento `<odc:ConnectionString>`, role até o final da linha e exclua `Embedded Data=False` e, em seguida, exclua `Edit Mode=0`. Se o último caractere da cadeia de caracteres for um ponto-e-vírgula, exclua-o agora.  
  
7.  Salve o arquivo. As etapas restantes dependem da versão do PowerPivot e do Excel que você está usando.  
  
8.  1.  Inicie o Excel 2013  
  
    2.  Na faixa de opções **PowerPivot** , clique em **Gerenciar**.  
  
    3.  Clique em **Obter Dados Externos** e clique em **Conexões existentes**.  
  
    4.  Clique no arquivo .ODC, caso ele seja exibido. Se o arquivo .ODC não for exibido, clique em **Procurar Mais** e, no caminho do arquivo, especifique o arquivo .odc.  
  
    5.  Clique em **Abrir**  
  
    6.  Clique em **Testar Conexão** para verificar se a conexão é estabelecida com êxito.  
  
    7.  Digite um nome para a conexão e clique em **Avançar**.  
  
    8.  Em especificar consulta MDX, clique em **Design** para abrir o designer de consulta MDX e montar os dados que você deseja trabalhar **se você vir a mensagem de erro** "o nome da propriedade modo de edição não é formatado corretamente.", verifique se você as edições do. Arquivo ODC.  
  
    9. Clique em **OK** e em **Concluir**.  
  
    10. Crie os relatórios de Tabela Dinâmica ou Gráfico Dinâmico para visualizar os dados no Excel.  
  
9. 1.  Inicie o Excel 2010.  
  
    2.  Na faixa de opções PowerPivot, clique em **Abrir Janela do PowerPivot**.  
  
    3.  Na tira Design na janela do PowerPivot, clique em **Conexões existentes**.  
  
    4.  Clique em **Procurar mais**.  
  
    5.  No caminho do arquivo, especifique o arquivo .odc.  
  
    6.  Clique em **Abrir**. O Assistente de Importação de Tabelas é iniciado, usando a cadeia de caracteres de conexão com a pasta de trabalho PowerPivot que contém os dados de uso.  
  
    7.  Clique em **Testar a conexão** para verificar se você tem acesso.  
  
    8.  Digite um nome intuitivo para a conexão e, em seguida, clique em **Avançar**.  
  
    9. Em Especificar Consulta MDX, clique em **Design** para abrir o designer de consulta MDX e montar os dados com os quais deseja trabalhar. Em seguida, crie relatórios de Tabela Dinâmica ou Gráfico Dinâmico para visualizar os dados no Excel.  
  
## <a name="see-also"></a>Consulte também  
 [Atualização de dados do PowerPivot com SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
