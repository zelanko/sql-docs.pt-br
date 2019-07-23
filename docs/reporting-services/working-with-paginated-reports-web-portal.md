---
title: Trabalhando com relatórios paginados (portal da Web) | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: fb0bc38f-dc56-4350-8457-cd135c0346e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0516adde38fc7f6e9cc1b4e20bc9beef76a4df22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68222656"
---
# <a name="working-with-paginated-reports-web-portal"></a>Trabalhando com relatórios paginados (portal da Web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Você pode exibir e gerenciar as propriedades de um relatório paginado dentro do portal da Web. O portal da Web pode iniciar o Construtor de Relatórios para criar ou editar relatórios paginados.  
   
## <a name="create-a-paginated-report"></a>Criar um relatório paginado  
  
Para criar um novo conjunto de dados compartilhado, você pode fazer o seguinte.  
  
1.  Selecione Novo na barra de menus.  
  
2.  Selecione **Relatório Paginado**.  
  
    ![ssRSWebPortal-new-report](../reporting-services/media/ssrswebportal-new-report.png)  
  
3.  Isso iniciará o Construtor de Relatórios ou solicitará que você o baixe.  
  
4.  Crie seu relatório e selecione o ícone **salvar** no canto superior esquerdo para salvar o relatório paginado de volta no servidor de relatório.  
  
## <a name="manage-an-existing-paginated-report"></a>Gerenciar um relatório paginado existente  
  
Para gerenciar um relatório paginado existente, você pode fazer o seguinte.  
  
> [!NOTE]
> Se os relatórios paginados não aparecerem na pasta, verifique se você visualizando os relatórios paginados. Você pode selecionar **Modo de Exibição** na barra de menus na parte superior direita do portal da Web. Certifique-se de que a opção **Relatórios paginados** está marcada.  
  
1.  Selecione as **reticências (...)** do conjunto de dados que deseja gerenciar.  
      
    ![ssRSWebPortal-manage-report1](../reporting-services/media/ssrswebportal-manage-report1.png)  
  
2.  Selecione **Gerenciar** , o que levará você até a tela de edição.  
    
    ![ssRSWebPortal-manage-report2](../reporting-services/media/ssrswebportal-manage-report2.png)  
  
## <a name="properties"></a>Propriedades  
  
Na tela de propriedades, você pode alterar o **nome** a e **descrição** do relatório paginado. Você também pode **Excluir**, **Mover**, **Criar um relatório vinculado**, **Editar no Construtor de Relatórios**, **Baixar** ou **Substituir**.  
    
![ssRSWebPortal-report-properties](../reporting-services/media/ssrswebportal-report-properties.png)  
   
## <a name="parameters"></a>Parâmetros  
  
Você pode modificar os parâmetros existentes de um relatório paginado. Para adicionar um novo parâmetro, você deve editar o relatório no Construtor de Relatórios ou no SQL Server Data Tools.  
  
![ssRSWebPortal-report-parameters](../reporting-services/media/ssrswebportal-report-parameters.png)  
   
## <a name="data-source"></a>fonte de dados  
Você pode apontar para uma fonte de dados compartilhada ou inserir informações de conexão para uma fonte de dados personalizada.  
  
![ssRSWebPortal-relatório de datasource](../reporting-services/media/ssrswebportal-report-datasource.png)  
  
As opções a seguir são usadas para especificar uma fonte de dados personalizada.  
  
**Tipo**  
  
Especifique uma extensão de processamento de dados usada para processar dados da fonte de dados. Para obter uma lista de extensões de dados internas, consulte [Fontes de dados com suporte no Reporting Services (SSRS)]. Extensões de processamento de dados adicionais podem estar disponíveis em fornecedores de terceiros.  
  
**Cadeia de conexão**  
  
Especifique a cadeia de conexão que o servidor de relatório utiliza para conectar-se à fonte de dados. O tipo de conexão determina a sintaxe que você deve usar. Por exemplo, uma cadeia de caracteres de conexão da extensão do processamento de dados XML é uma URL para um documento XML. Na maioria dos casos, uma cadeia de caracteres de conexão típica especifica o servidor de banco de dados e um arquivo de dados. O exemplo a seguir ilustra uma cadeia de conexão usada para se conectar a um banco de dados do SQL Server chamado MyData:  
  
    data source=(a SQL Server instance);initial catalog=MyData  
  
Uma cadeia de conexão pode ser configurada como uma expressão para que você possa especificar a fonte de dados em tempo de execução. Expressões de fonte de dados são definidas no relatório, no Designer de Relatórios. Expressões de fonte de dados não podem ser definidas, exibidas ou modificadas no portal da Web. Porém, você pode substituir uma expressão de fonte de dados clicando em **Substituir Padrão** para digitar uma cadeia de conexão estática. Se você quiser retornar à expressão, clique em **Reverter em Padrão**. O servidor de relatórios armazena a cadeia de caracteres de conexão original no caso de você precisar restaurá-la. Para usar expressões de fonte de dados, você deve usar as informações de conexão de fonte de dados publicadas originalmente no relatório. As fontes de dados compartilhadas não dão suporte ao uso de expressões na cadeia de conexão.  
  
**Credenciais**  
  
Você pode especificar a opção que determina como as credenciais são obtidas.  
  
> [!IMPORTANT]
> Se forem fornecidas credenciais na cadeia de conexão, serão ignorados as opções e os valores fornecidos nesta seção. Observe que, se você especificar as credenciais na cadeia de conexão, os valores serão exibidos em texto não criptografado para todos os usuários que exibirem essa página.  
  
**Como o usuário que está visualizando o relatório**  
  
Use as credenciais do Windows do usuário atual para acessar a fonte de dados. Selecione essa opção quando as credenciais usadas para acessar a fonte de dados forem as mesmas que as usadas para fazer logon no domínio de rede. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se o Kerberos não estiver habilitado, as credenciais do Windows não poderão ser passadas para outro serviço ou para o computador remoto. Se forem necessárias conexões de computador adicionais, ocorrerá um erro em vez da exibição dos dados esperados.  
  
Um administrador de servidor de relatórios pode desabilitar o uso da segurança integrada do Windows para acessar fontes de dados de relatório. Se esse valor estiver esmaecido, o recurso não estará disponível.  
  
Não use essa opção se você planeja programar ou assinar a esse relatório. Processamento de relatório programado ou autônomo requer credenciais que podem ser obtidas sem entrada de usuário ou contexto de segurança de um usuário atual. Somente credenciais armazenadas fornecem esse recurso. Por esse motivo, o servidor de relatórios evita que você agende relatório ou processe assinatura, se o relatório estiver configurado para tipo de credencial de segurança integrada do Windows. Se você escolher essa opção para um relatório já assinado ou com operações agendadas, as operações de assinatura e agendamento serão interrompidas.  
  
**Usando essas credenciais**  
  
Armazene um nome de usuário criptografado e a senha no banco de dados do servidor de relatórios. Selecione essa opção para executar um relatório autônomo (por exemplo, relatórios iniciados por agendas ou eventos em vez de pela ação do usuário).   
  
Você também pode escolher que tipo de credencial seria. Autenticação do Windows (nome de usuário e senha do Windows) ou uma credencial de banco de dados específico (nome de usuário e senha) como a autenticação do SQL.  
  
Se a conta for uma credencial do Windows, ela deverá ter permissões locais de logon no computador que hospeda a fonte de dados usada pelo relatório.  
  
Selecione **Faça logon usando essas credenciais, mas depois tente representar o usuário que está exibindo o relatório** para permitir delegação de credenciais, mas somente se uma fonte de dados dá suporte à representação. No caso de bancos de dados do SQL Server, essa opção define a função SETUSER. Para o Analysis Services, ele usa EffectiveUserName.  
  
**Solicitando as credenciais ao usuário que está visualizando o relatório**  
  
Cada usuário deve digitar um nome de usuário e uma senha para acessar a fonte de dados. Você pode definir o texto do prompt que solicita as credenciais do usuário. Por exemplo, "Digite ou insira um nome de usuário e uma senha para acessar a fonte de dados."  
  
Você também pode escolher que tipo de credencial seria. Autenticação do Windows (nome de usuário e senha do Windows) ou uma credencial de banco de dados específico (nome de usuário e senha) como a autenticação do SQL.  
  
**Sem nenhuma credencial**  
  
Isso permite a você não fornecer nenhuma credencial para a fonte de dados. Se uma fonte de dados precisar de um logon de usuário, a escolha dessa opção não terá nenhum efeito. Você só deve escolher esta opção se a conexão de fonte de dados não requerer credenciais de usuário.  
  
Para usar essa opção, a conta de execução autônoma deve estar previamente configurada para o seu servidor de relatório. A conta de execução autônoma é usada para conectar a fontes externas, quando outros cursos de credenciais não estiverem disponíveis. Se você especificar essa opção e a conta não estiver configurada, a conexão com a fonte de dados do relatório falhará e o processamento do relatório não ocorrerá. Para obter mais informações sobre essa conta, consulte [Configurar a conta de execução autônoma (Gerenciador de Configuração do SSRS)](../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="subscriptions"></a>Assinaturas  
Uma assinatura do Reporting Services é uma configuração que fornece um relatório em um momento específico ou em resposta a um evento, em um formato de arquivo que você especificar. Por exemplo, toda quarta-feira, salvar o relatório MonthlySales.rdl como um documento do Microsoft Word em um compartilhamento de arquivo. As assinaturas podem ser usadas para agendar e automatizar a entrega de um relatório e com um conjunto específico de valores de parâmetros do relatório. Para obter mais informações, consulte [Trabalhando com assinaturas](working-with-subscriptions-web-portal.md).
  
![ssRSWebPortal-report-subscription1](../reporting-services/media/ssrswebportal-report-subscription1.png)
   
## <a name="dependent-items"></a>Itens Dependentes  
Use a página Itens Dependentes para exibir uma lista de itens que fazem referência a este relatório. O ícone para cada tipo de item indica do que se trata. Em seguida, selecione as **reticências (...)** em cada item para gerenciar esses itens mais detalhadamente.  
  
## <a name="caching"></a>Cache  
Quando o assunto é armazenar dados em cache para um relatório paginado, há opções. Você começará com uma simples seleção.  
  
1.  **Sempre executar este relatório com os dados mais recentes** emitirá as consultas à fonte de dados sempre que você executar o relatório. Isso resulta em um relatório sob demanda que contém os dados mais atualizados. Uma nova instância do relatório será criada sempre que o relatório for aberto e ela conterá os resultados de uma nova consulta. Com essa abordagem, se dez usuários abrirem o relatório simultaneamente, dez consultas serão enviadas à fonte de dados para processamento.  
  
2.  **Armazenar cópias deste relatório em cache e utilizá-las quando disponíveis** inserirá uma cópia temporária dos dados em um cache para uso futuro. O cache normalmente melhora o desempenho porque os dados são retornados do cache, em vez de haver uma nova execução da consulta de conjunto de dados. Com essa abordagem, se dez usuários abrirem o relatório, somente a primeira solicitação resultará uma consulta à fonte de dados. O relatório é subsequentemente armazenado em cache e os demais nove usuários visualizam o relatório armazenado em cache.  
  
3.  **Sempre executar esse relatório contra instantâneos gerados previamente** armazenará os dados e o layout do relatório em cache durante um determinado período de tempo. Você pode executar um relatório como instantâneo de relatório para evitar que o relatório seja executado em momentos arbitrários (durante um backup agendado, por exemplo). O instantâneo pode ser atualizado em uma agenda. [Saiba mais]  
  
![ssRSWebPortal-report-caching1](../reporting-services/media/ssrswebportal-report-caching1.png)  
   
A seleção de **Armazenar cópias deste relatório em cache e utilizá-las quando disponíveis** apresentará algumas opções adicionais.  
  
![ssRSWebPortal-report-caching2](../reporting-services/media/ssrswebportal-report-caching2.png)  

Para obter mais informações, consulte [Trabalhando com instantâneos](working-with-snapshots-web-portal.md).
  
### <a name="cache-expiration"></a>Validade do cache  
  
Você pode controlar se deseja expirar o cache do relatório paginado após um determinado período, ou se prefere fazer isso com base em uma agenda. Você pode usar uma agenda compartilhada  
  
> [!NOTE]
> Isso não atualiza o cache.  
  
### <a name="cache-refresh-plans"></a>Planos de atualização do cache  
  
Você pode usar os Planos de Atualização do Cache para criar agendas de pré-carregamento do cache com cópias temporárias de dados para um relatório paginado. Um plano de atualização inclui uma agenda e a opção para especificar ou substituir valores de parâmetros. Você não pode substituir valores de parâmetros que estão marcados como somente leitura. Você pode criar e usar mais de um plano de atualização.  
   
As atribuições padrão de função que permitem adicionar, excluir e alterar relatórios paginados para planos de atualização de cache são Gerenciador de Conteúdo, Meus Relatórios e Publicador.  
  
Depois de aplicar a opção de cache acima, você pode definir um plano de atualização do cache. Para fazer isso, escolha o link **Gerenciar Planos de Atualização** que aparece depois de aplicar as configurações de cache. Isso o levará até a página de plano de atualização do cache.   
  
Para criar um novo plano de atualização de cache, escolha **Novo Plano de Atualização do Cache**. Em seguida, você pode inserir um nome para o plano e especificar uma agenda. Se o conjunto de dados tiver parâmetros definidos, você verá os listados e será capaz de fornecer valores, a menos que estejam marcados como somente leitura.  
  
Quando terminar, selecione **Criar Plano de Atualização do Cache**.  
  
![ssRSWebPortal-report-caching3](../reporting-services/media/ssrswebportal-report-caching3.png)  
  
> [!NOTE]
> O SQL Server Agent precisa estar em execução para criar um plano de atualização do cache.  
  
Em seguida, você pode **Editar** ou **Excluir** os planos listados. A opção **Novo Com Base Em Existente** é habilitada quando um, e apenas um, plano de atualização do cache for selecionado. Essa opção criará um novo plano de atualização que é copiado do plano original. A página Plano de Atualização do Cache é aberta pré-populada com detalhes do plano que foi selecionado. Você pode modificar as opções do plano de atualização e salvar o plano com uma nova descrição.  
  
## <a name="history-snapshots"></a>Instantâneos de histórico  
  
Use a página Instantâneos de Histórico para exibir instantâneos de relatórios gerados e armazenados ao longo do tempo. Dependendo das opções definidas, o histórico do relatórios poderá conter somente os instantâneos mais recentes.  
  
O histórico de relatório é sempre exibido no contexto do relatório de origem. Você não pode exibir o histórico de todos os relatórios em um servidor de relatórios em um único lugar.  
  
Para gerar um instantâneo, o relatório deve ser executado de modo autônomo (ou seja, ele deve usar credenciais armazenadas; relatórios com parâmetros devem conter valores de parâmetro padrão para todos os parâmetros). Os instantâneos podem ser gerados manualmente ou como uma operação agendada.   
  
Você pode clicar em um instantâneo de histórico de relatórios para exibi-lo. Instantâneos exibidos em histórico de relatórios só são diferenciados pela data e hora em que foram criados. Não existe indicação visual para distinguir se um relatório foi gerado em resposta a uma operação programada ou manual.  
  
## <a name="security"></a>Segurança  
Use a página Propriedades de Segurança para exibir ou modificar as definições de segurança que determinam o acesso ao relatório. Essa página está disponível para itens que você tem permissão para proteger.  
  
O acesso aos itens é definido por atribuições de função que especificam as tarefas que um grupo ou usuário podem executar. Uma atribuição de função consiste em um nome de usuário ou grupo e em uma ou mais definições de função que especificam uma coleção de tarefas.  
  
**Editar Segurança de Item**  
  
Selecione para alterar a maneira como a segurança é definida para o item atual.

## <a name="next-steps"></a>Próximas etapas

[Portal da Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabalhar com conjuntos de dados compartilhados](../reporting-services/work-with-shared-datasets-web-portal.md)

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
