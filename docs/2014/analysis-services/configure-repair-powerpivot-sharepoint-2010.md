---
title: Configurar ou reparar o PowerPivot para SharePoint 2010 (ferramenta de configuração do PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d61f49c5-efaa-4455-98f2-8c293fa50046
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a80e362c97df74773d303a4b022d376fff40fb70
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360338"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2010-powerpivot-configuration-tool"></a>Configurar ou reparar o PowerPivot para SharePoint 2010 (Ferramenta de Configuração do PowerPivot)
  Para configurar ou reparar uma instalação do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerPivot para SharePoint 2010, use a Ferramenta de Configuração do PowerPivot. A ferramenta de configuração começa examinando o sistema e retorna uma lista de ações necessárias para concluir ou reparar uma instalação. O assistente de configuração do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] instala a Ferramenta de Configuração do PowerPivot para SharePoint 2010, bem como a Ferramenta de Configuração do PowerPivot para SharePoint 2013. Este tópico descreve a Ferramenta de Configuração do PowerPivot para SharePoint 2010. Para obter mais informações sobre o SharePoint 2010, consulte [configurar ou reparar o PowerPivot para SharePoint 2013 &#40;ferramenta de configuração do PowerPivot&#41;](power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md).  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 
  
##  <a name="bkmk_before"></a> Antes de iniciar  
 A Ferramenta de Configuração PowerPivot para SharePoint 2010 examina arquivos de programas, configurações do Registro e portas disponíveis. Para aproveitar ao máximo as ferramentas, examine os requisitos a seguir.  
  
-   Requisitos gerais para executar a ferramenta de configuração [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
-   O PowerPivot para SharePoint 2010 requer aplicativos Web configurados para a autenticação de modo clássico. Se a Ferramenta de Configuração PowerPivot para SharePoint 2010 criar o aplicativo para você, o aplicativo será configurado para o modo clássico.  
  
-   A porta 80 precisa estar disponível; uma das tarefas selecionadas exige que a ferramenta de configuração crie e configure um aplicativo Web.  
  
##  <a name="bkmk_using"></a> Usando a ferramenta de configuração do PowerPivot  
 A primeira página da ferramenta fornece um resumo dos valores de entrada usados para configurar o farm do SharePoint. Além dos valores de entrada que você fornece, são usados valores padrão para configurar o sistema. Os nomes padrão são usados para aplicativos de serviço, bancos de dados de aplicativo de serviço e propriedades de aplicativo de serviço.  
  
> [!TIP]  
>  Se a Ferramenta de Configuração do PowerPivot verificar o computador e retornar uma lista de tarefas em branco no painel esquerdo, nenhum recurso ou configuração precisará ser definido. Para alterar a configuração do SharePoint ou do PowerPivot, use o Windows PowerShell ou páginas de gerenciamento na Administração Central do SharePoint. Para obter mais informações, consulte [administração de servidor do PowerPivot e a configuração na Administração Central](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Os valores para contas de serviço são usados para vários serviços. Por exemplo, a Ferramenta de Configuração do PowerPivot usa a conta padrão na primeira página para definir todas as identidades do pool de aplicativos. Você pode alterar estas contas posteriormente modificando as propriedades de aplicativo de serviço em Administração Central.  
  
-   A exceção a essa regra na Ferramenta de Configuração do PowerPivot para SharePoint 2010 é a conta de serviço do Analysis Services. Essa conta é especificada durante a instalação e você digitar uma senha para essa conta de **registrar o SQL Server Analysis Services (PowerPivot no servidor Local)** ação. A página resumida não inclui um campo para esta senha; portanto, insira-a na página para aquela ação.  
  
 A ferramenta fornece uma interface com guias que inclui entradas de parâmetros, script do Windows PowerShell e mensagens de status.  
  
 A Ferramenta de Configuração do PowerPivot usa o Windows PowerShell para configurar o servidor. Você pode clicar na **Script** guia para examinar o script do Windows PowerShell o.  
  
 ![Interface de usuário da ferramenta de configuração](media/ssas-pctui.gif "interface de usuário da ferramenta de configuração")  
  
##  <a name="bkmk_steps"></a> Etapas de configuração  
 O link para a ferramenta de configuração fica visível apenas quando o PowerPivot para SharePoint 2010 está instalado no servidor local.  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e em **Ferramenta de Configuração do PowerPivot**.  
  
2.  Clique em **Configurar ou Reparar o PowerPivot para SharePoint**.  
  
3.  Expanda a janela para o tamanho total. Você verá uma barra de botões na parte inferior da janela que inclui os comandos **Validar**, **Executar**e **Sair** .  
  
4.  **Conta padrão:** Na guia parâmetros, digite uma conta de usuário de domínio para o **nome de usuário de conta padrão**. Esta conta é usada para provisionar serviços essenciais, inclusive o pool de aplicativos do serviço PowerPivot. Não especifique uma conta interna, como Serviço de Rede ou Sistema Local. A ferramenta bloqueia configurações que especificam contas internas.  
  
     **Frase Secreta:** digite uma frase secreta. Para um novo farm do SharePoint, a frase secreta é usada sempre que um novo servidor ou aplicativo é adicionado ao farm do SharePoint. Se ele for um farm existente, insira a frase secreta que permite adicionar um aplicativo de servidor ao farm.  
  
5.  **Porta:** opcionalmente, digite um número da porta para se conectar ao aplicativo Web Administração Central ou use o número fornecido, gerado aleatoriamente. A ferramenta de configuração verifica se o número está disponível antes de oferecê-lo como opção.  
  
6.  Clique em **registrar o SQL Server Analysis Services (PowerPivot) no servidor Local**.  
  
     Insira a senha da conta de serviço do Analysis Services.  
  
7.  Opcionalmente, revise os valores de entrada restantes usados para concluir cada ação. Para obter mais informações sobre cada um, consulte [Valores de entrada usados para configurar o servidor](#bkmk_input) neste tópico.  
  
8.  Opcionalmente, remova as ações que você não deseja processar. Por exemplo, se desejar configurar o Serviço de Repositório Seguro, clique em **Configurar Serviço de Repositório Seguro**e desmarque a caixa de seleção **Inclua esta ação na lista de tarefas**.  
  
9. Clique em **Validar** para verificar se a ferramenta tem informações suficientes para processar as ações na lista.  
  
    > [!NOTE]  
    >  Se ocorrer um erro de configuração de farm, isso pode ser porque o Servidor do SharePoint 2010 SP1 não está instalado.  
  
10. Clique em **Executar** para processar todas as ações na lista de tarefas. O botão **Executar** é habilitado após a validação das ações. Se **Executar** não estiver habilitado, clique em **Validar** primeiro.  
  
11. [Verify a PowerPivot for SharePoint Installation](instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_input"></a> Valores de entrada usados para configurar o servidor  
 A Ferramenta de Configuração do PowerPivot usa uma combinação de valores de entrada que você digita e valores padrão que ele detecta ou usa automaticamente.  
  
 A lista de ações na ferramenta de configuração depende da configuração atual dos farms do SharePoint. Por exemplo, se o farm do SharePoint já estiver configurado, nenhuma ação será listada na ferramenta. Você pode executar a ferramenta a qualquer momento para configurar, reparar ou detectar erros de configuração. Se os serviços obrigatórios como Serviços do Excel ou Serviço de Repositório Seguro não estão sendo executados no farm, a ferramenta detectará os serviços ausentes e fornecerá opções para habilitá-los. Se nenhuma ação for necessária, a lista de tarefas estará vazia.  
  
 A tabela a seguir descreve os valores que são usados para configurar o servidor.  
  
|Página|Valor de entrada|Origem|Descrição|  
|----------|-----------------|------------|-----------------|  
|**Configurar ou reparar o PowerPivot para SharePoint**|Conta padrão|Usuário atual|A conta padrão é uma conta de usuário de domínio do Windows que é usada para provisionar serviços compartilhados no farm. É usado para provisionar o aplicativo de serviço PowerPivot, Serviço de Repositório Seguro, Serviços do Excel, a identidade de pool de aplicativo Web, o administrador da coleção de sites e a conta autônoma de atualização de dados PowerPivot.<br /><br /> Por padrão, a ferramenta insere a conta de domínio do usuário atual. A menos que você esteja configurando um servidor para propósitos de avaliação, deve substituí-lo por uma conta de usuário de domínio diferente.<br /><br /> Posteriormente, também será possível alterar as identidades do serviço, usando a Administração Central.<br /><br /> Opcionalmente, na ferramenta de Configuração do PowerPivot, você pode especificar contas dedicadas para o seguinte:<br /><br /> Aplicativo Web, usando o **criar aplicativo Web padrão** página (supondo que a ferramenta esteja criando um aplicativo web para o farm).<br /><br /> PowerPivot para conta de atualização de dados autônoma, usando o **criar conta autônoma para atualização de dados** página nessa ferramenta.|  
||Servidor de Banco de Dados|Instância nomeada local do PowerPivot, se houver.|Se uma instância de mecanismo de banco de dados for instalada como uma instância nomeada do PowerPivot, a ferramenta populará o campo de servidor de banco de dados com esta instância. Se você não instalou o mecanismo de banco de dados, este campo estará vazio. Você deve fornecer uma instância. Pode ser qualquer versão ou edição de SQL Server que tenha suporte para farms do SharePoint.|  
||Frase Secreta|Entradas de usuário|Se estiver criando um novo farm, a frase secreta que você inserir será a frase secreta para o farm. Se você estiver adicionando o PowerPivot para SharePoint a um farm existente, você deverá fornecer a frase secreta que foi definida para o farm quando foi criado.|  
||Porta da Administração Central do SharePoint|Padrão, se necessário|Se o farm não estiver configurado, a ferramenta fornecerá opções para criar o farm, inclusive um ponto de extremidade HTTP para a Administração Central. O padrão é um número de porta gerado aleatoriamente que não está em uso.|  
|**Configurar Novo Farm**|Servidor de Banco de Dados<br /><br /> Conta do Farm<br /><br /> Frase Secreta<br /><br /> Porta da Administração Central do SharePoint|Padrão, se necessário|O padrão das configurações é o valor inserido na página principal.|  
|**Configurar a instância de serviço Local**|Senha da conta de serviço do Analysis Services|Entradas de usuário|Você deve digitar a senha da conta de serviço do Analysis Services na **registrar o SQL Server Analysis Services (PowerPivot) no servidor Local** página.<br /><br /> A conta de serviço foi especificada durante a instalação. Você agora deve digitar a senha como uma entrada para registrar a instância de serviço local com o SharePoint.|  
|**Criar aplicativo de serviço PowerPivot**|Nome do aplicativo do serviço PowerPivot|Padrão|O nome padrão é Aplicativo de Serviço PowerPivot Padrão. Você pode substituir um valor diferente na ferramenta.|  
||Servidor do banco de dados do aplicativo de serviço PowerPivot|Padrão|O servidor de banco de dados que hospeda o banco de dados do aplicativo de serviço PowerPivot. O nome do servidor padrão é o mesmo servidor de banco de dados usado para o farm. Você pode substituir um valor diferente na ferramenta.|  
||Nome do banco de dados do aplicativo de serviço PowerPivot|Padrão|O nome de banco de dados padrão é baseado no nome de aplicativo de serviço, seguido por um GUID para garantir um nome exclusivo. Você pode substituir um valor diferente na ferramenta.|  
||Atualizar pastas de trabalho para habilitar atualização de dados|Entradas de usuário|A atualização de dados falha e não tem suporte para pastas de trabalho PowerPivot do SQL Server 2008 R2. A opção **refresh atualizar pastas de trabalho para habilitar dados** atualiza as pastas de trabalho para a versão do SQL Server 2012 PowerPivot.|  
|**Criar Aplicativo Web Padrão**|Nome do Aplicativo Web|Padrão, se necessário|Se nenhum aplicativo Web existir, a ferramenta criará um. O aplicativo web será configurado para autenticação de modo clássico e escutar **, a porta 80**. O tamanho máximo de carregamento de arquivo é definido como 2047 MB, o máximo permitido pelo SharePoint. O maior tamanho de carregamento de arquivo é acomodar arquivos grandes do PowerPivot.|  
||URL|Padrão, se necessário|A ferramenta cria uma URL baseada no nome do servidor, usando as mesmas convenções de nomenclatura de arquivo que o SharePoint.|  
||Pool de Aplicativos Web|Padrão, se necessário|A ferramenta cria um pool de aplicativos padrão no IIS.|  
||Conta e Senha do Pool de Aplicativos Web|Padrão, se necessário|A conta do pool de aplicativos é baseada na conta padrão, mas você pode substituí-la na ferramenta.|  
||Servidor de banco de dados de aplicativo Web|Padrão, se necessário|A instância de banco de dados padrão é pré-selecionada para armazenar o banco de dados de aplicativo, mas você pode especificar uma instância do SQL Server diferente na ferramenta.|  
||Nome do banco de dados de aplicativo Web|Padrão, se necessário|O nome de banco de dados é baseado nas convenções de nomenclatura de arquivo de SharePoint, mas você pode escolher um nome diferente.|  
|**Implantar Solução de Aplicativo Web**|URL|Padrão, se necessário|A URL padrão é do aplicativo Web padrão.|  
||Tamanho Máximo do Arquivo (em MB)|Padrão, se necessário|A configuração padrão é 2047. As bibliotecas de documentos do SharePoint também têm um tamanho máximo e a configuração do PowerPivot não deve exceder a configuração da biblioteca de documentos. Para obter mais informações, consulte [configurar o tamanho máximo do arquivo de carregamento &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).|  
|**Criar Coleção de Sites**|Administrador do Site|Padrão, se necessário|A ferramenta usa a conta padrão. Você pode anulá-la na página **Criar Coleção de Sites** .|  
||Contact Email|Padrão, se necessário|Se o Microsoft Outlook estiver configurado no servidor, a ferramenta usará o endereço de email do usuário atual. Caso contrário, um valor de espaço reservado será usado.|  
||URL de site|Padrão, se necessário|A ferramenta cria uma URL de site, usando as mesmas convenções de nomenclatura de URL que o SharePoint.|  
||Título do site|Padrão, se necessário|A ferramenta adiciona o **Site do PowerPivot** como o título padrão.|  
|**Ativar recurso do PowerPivot em um conjunto de sites**|URL de site||URL da coleção de sites para a qual você está ativando recursos do PowerPivot.|  
||Habilite o recurso premium para este site||Habilite o recurso de site do SharePoint "PremiumSite".|  
|**Criar Aplicativo de Serviço de Repositório Seguro**|Nome do Aplicativo de Serviço||Digite o nome do aplicativo do serviço de Repositório Seguro.|  
||Servidor de Banco de Dados||Digite o nome do servidor de banco de dados a ser usado para o aplicativo de serviço de Repositório Seguro.|  
|**Criar Proxy de Aplicativo de Serviço de Repositório Seguro**|Nome do Aplicativo de Serviço||Digite o nome do aplicativo do serviço de Repositório Seguro.|  
||Proxy de aplicativo de serviço||Digite o nome do proxy de aplicativo do serviço de Repositório Seguro.  O nome aparecerá no grupo de conexões padrão que associa aplicativos a aplicativos Web de conteúdo do SharePoint.|  
|**Atualizar Chave Mestra do Serviço de Repositório Seguro**|Proxy de aplicativo de serviço||Digite o nome do proxy de aplicativo do serviço de Repositório Seguro|  
||Frase Secreta||A chave mestra é usada para criptografia de dados. Por padrão, a frase secreta usada para gerar a chave é a mesma que é usada para provisionar novos servidores no farm. Você pode substituir a frase secreta padrão por uma frase secreta exclusiva.|  
|**Criar conta autônoma para Datarefresh**|ID do Aplicativo de Destino||A ID do aplicativo pode ser um texto descritivo.|  
||Nome Amigável para Aplicativo de Destino|||  
||Nome de Usuário e Senha da Conta Autônoma||Digite as credenciais de uma conta de usuário do Windows que é usada pelo aplicativo de destino e é usada para executar a atualização de dados autônoma.|  
||URL de site||Digite a URL do site da coleção de sites associada ao aplicativo de destino. Para associar a coleções de sites adicionais, use a Administração Central do SharePoint.|  
|**Criar Aplicativo de Serviço dos Serviços do Excel**|Nome do Aplicativo de Serviço||Digite um nome de aplicativo de serviço. Um banco de dados do aplicativo de serviço com o mesmo nome será criado no servidor de banco de dados do farm do SharePoint.|  
|**Adicionar MSOLAP.5 como um provedor confiável**|Nome do Aplicativo de Serviço||Os Serviços do Excel no SharePoint 2010 usam o provedor OLE DB do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para se conectar a dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esta etapa adicionará a versão do provedor OLE DB instalado com o PowerPivot para SharePoint, como provedor confiável para Serviços do Excel.|  
||Nome do Servidor do PowerPivot|||  
|||||  
  
 Se a Ferramenta de Configuração do PowerPivot criar o farm, ela criará os bancos de dados exigidos no servidor de banco de dados, usando as mesmas convenções de nomenclatura de arquivo do SharePoint. Não é possível alterar o nome do banco de dados do farm.  
  
 Se a ferramenta criar uma coleção de sites, criará um banco de dados de conteúdo no servidor de banco de dados, usando as mesmas convenções de nomenclatura de arquivo que o SharePoint. Não é possível alterar o nome do banco de dados do conteúdo.  
  
##  <a name="bkmk_nextsteps"></a> Próximas etapas  
 Depois de concluir uma instalação do servidor, há várias tarefas pós-instalação a serem executadas:  
  
-   Conceder permissões do SharePoint a indivíduos e grupos. Essa tarefa é necessária para permitir o acesso a sites e conteúdo.  
  
-   Alterar as identidades do pool de aplicativos de serviço para execução em uma conta diferente. Especificar identidades diferentes para serviços e aplicativos é uma prática recomendada do SharePoint para uma implantação segura.  
  
-   Crie sites confiáveis adicionais nos Serviços do Excel para que seja possível variar as permissões e os parâmetros de configuração que funcionem melhor para o acesso de dados PowerPivot.  
  
-   Instale o ADO.NET Data Services 3.5 SP1 para habilitar a exportação de feed de dados de listas do SharePoint.  
  
-   Instale provedores de dados geralmente usados para habilitar a atualização de dados do lado do servidor.  
  
-   Baixe a ferramenta de criação do PowerPivot para a estação de trabalho para criar uma pasta de trabalho PowerPivot e publicá-la no SharePoint. Instalar a ferramenta e publicar uma pasta de trabalho PowerPivot conclui o ciclo de instalação com a verificação da interoperabilidade dos componentes de servidor recém-instalados.  
  
### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Conceder permissões do SharePoint a usuários de pastas de trabalho  
 Os usuários precisarão de permissões do SharePoint para publicar ou exibir pastas de trabalho. Certifique-se de conceder **modo de exibição** permissões para usuários que precisam exibir pastas de trabalho publicadas e **Contribute** permissões a usuários que publicam ou gerenciam pastas de trabalho. Você deve ser um administrador do conjunto de sites para conceder permissões.  
  
1.  No site, clique em **ações do Site**.  
  
2.  Clique em **permissões do Site**.  
  
3.  Crie grupos quando necessário se você desejar um conjunto de usuários com permissões **Colaborar** e outro grupo para um conjunto de usuários apenas com permissões **Exibir** .  
  
4.  Insira o usuário de domínio do Windows ou as contas do grupo que devem ter associação nos grupos. Como anteriormente, não use endereços de email ou grupos de distribuição se o aplicativo estiver configurado para autenticação clássica.  
  
### <a name="install-adonet-data-services-35-sp1"></a>Instale o ADO.NET Data Services 3.5 SP1  
 O ADO.NET Data Services é obrigatório para uma exportação do feed de dados das listas do SharePoint. O SharePoint 2010 não inclui esse componente no programa PrerequisiteInstaller, assim você deve instalá-lo manualmente.  
  
1.  Vá para a documentação de requisitos de hardware e software para o SharePoint 2010, [determinar requisitos de Hardware e Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  Em Instalando pré-requisitos de software, localize o link para o ADO.NET Data Services 3.5 que corresponde ao sistema operacional você está usando.  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Instalar provedores de dados usados na atualização de dados e verificar permissões de usuário  
 A atualização de dados do servidor permite que os usuários reimportem dados atualizados para suas pastas de trabalho no modo autônomo. Para que a atualização de dados seja bem-sucedida, o servidor deve ter o mesmo provedor de dados que foi usado originalmente para importar os dados. Além disso, a conta de usuário na qual a atualização de dados é executada frequentemente requer permissões de leitura nas fontes de dados externas. Verifique os requisitos para habilitar e configurar a atualização de dados para garantir êxito no resultado. Para obter mais informações, consulte [atualização de dados do PowerPivot com SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md).  
  
### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>Alterar o pool de aplicativos e as identidades de serviço no SharePoint  
 A ferramenta de Configuração do PowerPivot provisiona recursos do farm, aplicativos e serviços a serem executados em uma única conta. Isso simplifica a instalação, mas não resulta em uma implantação que atende aos requisitos de segurança de um farm do SharePoint. Para criar uma implantação mais robusta, altere os pools de aplicativos e as identidades de serviço para serem executados em contas diferentes após a conclusão da instalação. Para obter mais informações, consulte [configurar contas de serviço PowerPivot](power-pivot-sharepoint/configure-power-pivot-service-accounts.md).  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Crie sites de confiança adicionais nos Serviços do Excel  
 Você pode adicionar sites de confiança nos Serviços do Excel para variar as permissões e os parâmetros de configuração em sites que fornecem pastas de trabalho do Excel e dados PowerPivot. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na Administração Central](power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
### <a name="add-servers-or-applications"></a>Adicionar servidores ou aplicativos  
 Com o tempo, se você determinar a necessidade de armazenamento de dados e recursos de processamento adicionais, poderá adicionar uma segunda instância do servidor PowerPivot para SharePoint ao farm. Para obter instruções, consulte [lista de verificação de implantação: Expansão adicionando servidores do PowerPivot a um farm do SharePoint 2010](../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
## <a name="additional-resources"></a>Recursos adicionais  
 ![Configurações do SharePoint](media/as-sharepoint2013-settings-gear.gif "SharePoint Settings") [enviar comentários e informações de contato pelo Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de configuração do PowerPivot](power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [Administração e configuração de servidor do PowerPivot na Administração Central](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
