---
title: Configurar credenciais armazenadas para atualização de dados do PowerPivot (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 987eff0f-bcfe-4bbd-81e0-9aca993a2a75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73ee3f7f86203f4fa0ac2e4da86fecee0e2b4cf5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365069"
---
# <a name="configure-stored-credentials-for-powerpivot-data-refresh-powerpivot-for-sharepoint"></a>Configurar credenciais armazenadas para a atualização de dados PowerPivot (PowerPivot para SharePoint)
  Os trabalhos de atualização de dados PowerPivot podem ser executados em qualquer conta de usuário do Windows, desde que você crie um aplicativo de destino no Serviço de Repositório Seguro para armazenar as credenciais que deseja usar. Da mesma forma, se você desejar fornecer um logon de banco de dados que varie do um usado para importar os dados originalmente no PowerPivot para Excel, poderá mapear essas credenciais para um aplicativo de destino do Serviço de Repositório Seguro e, depois, especificar esse aplicativo de destino em uma agenda de atualização de dados.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 Após seguir as instruções deste tópico, você poderá usar a seguinte opção de credenciais na página agenda de atualização de dados PowerPivot:  
  
 ![SSAS_PowerPivotDataRefreshCreds_Stored](media/ssas-powerpivotdatarefreshcreds-stored.gif "SSAS_PowerPivotDataRefreshCreds_Stored")  
  
 Este tópico explica como configurar os nomes de usuários e as senhas que são usados para atualização de dados PowerPivot em um farm do SharePoint 2010. Antes de usar estas etapas, você deve ter habilitado o Serviço de Repositório Seguro e deve ter gerado uma chave mestra. Para obter mais informações, consulte [atualização de dados do PowerPivot com o SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 Este tópico contém as seguintes seções:  
  
 [Configurar qualquer conta do Windows para atualização de dados](#configAny)  
  
 [Configurar uma conta predefinida para acessar fontes de dados externas ou de terceiros](#config3rd)  
  
 Se você tiver problemas ao configurar ou usando a atualização de dados, consulte o [Troubleshooting PowerPivot Data Refresh](https://go.microsoft.com/fwlink/?LinkID=223279) página no wiki do TechNet para obter possíveis soluções.  
  
##  <a name="configAny"></a> Configurar qualquer conta do Windows para atualização de dados  
 Quando um usuário do SharePoint define uma agenda de atualização de dados, ele deve especificar a identidade do usuário com a qual a atualização de dados é executada. Entre as opções estão a seleção da conta autônoma de atualização de dados PowerPivot, a inserção de sua conta de usuário de domínio Windows ou a inserção de alguma outra conta de usuário do Windows que seja válida para fins de atualização de dados. As etapas desta seção destinam-se à última opção: especificar alguma outra conta do Windows.  
  
 Você pode escolher essa abordagem se desejar uma alternativa ao uso da conta autônoma de atualização de dados do PowerPivot (disponível para todos os usuários do PowerPivot no SharePoint) ou as credenciais do proprietário da pasta de trabalho. Por exemplo, você pode querer disponibilizar uma série de contas de atualização de dados para diferentes grupos de trabalho, com o objetivo de ajudar a acompanhar e gerenciar a atividade de atualização de dados no nível organizacional.  
  
> [!IMPORTANT]  
>  As pessoas e os aplicativos que usam esse aplicativo de destino (e as credenciais que ele armazena) devem ser listados como membros do aplicativo. Você deve adicionar a identidade de cada aplicativo de serviço PowerPivot que usará o aplicativo de destino, a sua conta do Windows e as contas de grupo ou usuário das pessoas que especificarão esse aplicativo de destino em suas agendas de atualização de dados. É possível especificar todas essas contas ao criar o aplicativo de destino. Se você não conhecer todas as contas de usuário e grupo que necessitarão de acesso a esse aplicativo, poderá adicioná-los posteriormente depois que o aplicativo de destino for criado.  
  
 Há 4 partes na configuração de credenciais armazenadas para a atualização de dados:  
  
-   Criar o aplicativo de destino que armazena as credenciais.  
  
-   Conceder permissões de colaboração à conta.  
  
-   Conceder as permissões de leitura da conta para acessar fontes de dados externas durante atualização de dados.  
  
-   Verifique se a atualização de dados funciona ao especificar este aplicativo de destino em uma agenda de atualização de dados.  
  
### <a name="step-1-create-a-target-application"></a>Etapa 1: Criar um aplicativo de destino  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **proteger o serviço de Store**.  
  
3.  Em gerenciar aplicativos de destino, clique em **New**.  
  
4.  Em ID do aplicativo de destino, digite uma cadeia de texto. Ela deve ser exclusiva, mas também fácil de lembrar. Os usuários digitarão essa cadeia de caracteres nas páginas da agenda de atualização de dados sempre que desejarem usar as credenciais armazenadas nesse aplicativo.  
  
5.  Em Nome para Exibição, digite um nome descritivo. Esse nome é usado somente para fins de exibição. Ele não é usado para especificar o aplicativo de destino em uma agenda de atualização de dados.  
  
6.  Em Email de Contato, digite seu endereço de email.  
  
7.  Em tipo de aplicativo de destino, selecione **grupo**.  
  
    > [!IMPORTANT]  
    >  A escolha de um tipo de conta de Grupo é necessária porque ela permite especificar todas as contas de usuário e serviço que solicitam acesso às credenciais. Para cada solicitação, o Serviço do Sistema PowerPivot verifica se o solicitante é membro do aplicativo de destino.  
  
8.  Ignore a URL da página do aplicativo de destino. A atualização de dados PowerPivot não usa essa URL.  
  
9. Clique em **Avançar**.  
  
10. No **especificam os campos de credenciais para o seu aplicativo de destino de Store seguro** página, aceite os valores padrão. Os nomes e tipos de campo devem ser Nome de Usuário do Windows e Senha do Windows.  
  
11. Clique em Avançar.  
  
12. Em Administradores de Aplicativo de Destino, especifique as contas de usuário de domínio do Windows de usuários do SharePoint que devem ter acesso administrativo às configurações de aplicativo de destino (por exemplo, a possibilidade de adicionar ou remover contas da lista Membros).  
  
13. Em Membros, adicione as contas de usuário e grupo a seguir:  
  
    1.  Como você está criando o aplicativo, acrescente sua conta de usuário do Windows à lista de Membros.  
  
    2.  Adicione a identidade do pool de aplicativos do aplicativo de serviço PowerPivot para permitir que ele recupere as credenciais quando a atualização de dados estiver agendada para ser executada. Para exibir a identidade do pool de aplicativos, vá para **gerenciar aplicativos de serviço**, selecione o aplicativo de serviço PowerPivot clicando no espaço vazio ao lado do nome (Isso seleciona a linha) e, em seguida, clique em **depropriedades**. A conta de segurança que aparece nessa página é aquela que deve ser adicionada como um membro do aplicativo de destino.  
  
    3.  Adicione as contas de usuário e grupo do Windows que irão inserir esse aplicativo de destino em agendas de atualização de dados.  
  
14. Clique em **OK**.  
  
15. Selecione o aplicativo de destino que você acabou de criar, clique na seta para baixo e selecione **definir credenciais.**  
  
16. Em Proprietário da Credencial, note que a lista de proprietários de credenciais é somente leitura. As contas com propriedade sobre as credenciais são os membros do aplicativo de destino. Para adicionar ou remover um proprietário de credencial, adicione ou remova contas da lista de membros do aplicativo de destino.  
  
     Em Nome do Usuário do Windows e Senha do Windows, digite as credenciais da conta de usuário Windows que será usada para executar a atualização de dados.  
  
17. Clique em **OK**.  
  
###  <a name="bkmk_grant"></a> Etapa 2: Conceder permissões de colaboração à conta  
 Para que você possa usar as credenciais armazenadas, a conta deve ter permissões de colaboração em qualquer pasta de trabalho PowerPivot para a qual seja usada. Esse nível de permissão é necessário para abrir a pasta de trabalho de uma biblioteca e, em seguida, salvá-la novamente na biblioteca após os dados serem atualizados.  
  
 Atribuir permissões é uma etapa executada pelo administrador da coleção de sites. Podem ser atribuídas permissões do SharePoint na coleção de sites raiz ou em qualquer nível abaixo desse, inclusive em documentos e itens individuais. A forma como você define permissões irá variar dependendo do quanto elas precisam ser granulares. As etapas a seguir mostram uma abordagem para conceder permissões.  
  
1.  Em um site do SharePoint, em ações do Site, clique em **permissões de Site**.  
  
2.  Clique em **Conceder Permissões**.  
  
3.  Em Selecionar usuários, digite o nome da conta de usuário do domínio Windows que você especificou no aplicativo de destino.  
  
4.  Em conceder permissões, selecione **conceder permissão a usuários diretamente**.  
  
5.  Selecione **Contribute**e, em seguida, clique em **Okey**.  
  
###  <a name="bkmk_dbread"></a> Etapa 3: Conceder permissões para acessar fontes de dados externas usadas na atualização de dados de leitura  
 Ao importar dados para uma pasta de trabalho PowerPivot, as conexões com dados externos são frequentemente baseadas em conexões confiáveis ou em conexões representadas que usam a identidade do usuário atual para conectar-se à fonte de dados. Estes tipos de conexões funcionam apenas quando o usuário atual tem permissão para ler os dados que está importando.  
  
 Em um cenário de atualização de dados, a mesma cadeia de conexão que foi usada para importar os dados é agora reutilizada para atualizar os dados. Se a cadeia de conexão assumir o usuário atual (por exemplo, uma cadeia de caracteres que inclua Integrated_Security=SSPI), o Serviço do Sistema PowerPivot passará a identidade do usuário especificada no aplicativo de destino como o usuário atual. Essa conexão terá êxito apenas se a conta tiver permissões de leitura na fonte de dados externa.  
  
 Por isso, conceda permissões somente leitura à conta em todas as fontes de dados externas usadas durante a atualização de dados.  
  
 Se você for administrador das fontes de dados usadas em sua organização, poderá criar um logon e atribuir as permissões necessárias. Caso contrário, você deverá entrar em contato com os proprietários dos dados e fornecer as informações da conta. Especifique a conta de usuário do domínio Windows que é mapeada para o aplicativo de destino. Essa é a conta que você especificou na "etapa 1: Criar um aplicativo de destino"neste tópico.  
  
###  <a name="bkmk_verify"></a> Etapa 4: Verificar a disponibilidade da conta em páginas de configuração de atualização de dados  
  
1.  Abra uma página de configuração de atualização de dados para uma pasta de trabalho publicada que contém dados do PowerPivot. Para obter instruções sobre como abrir a página, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
2.  Verifique se que o **conectar-se usando as credenciais salvas no Secure Store SSS (serviço) para fazer logon na fonte de dados** opção está habilitada na página de configuração de atualização de dados e, em seguida, insira o nome do aplicativo de destino.  
  
3.  Selecione o **também atualizar o mais rápido possível** caixa de seleção e, em seguida, clique em **Okey**.  
  
4.  Na biblioteca que contém a pasta de trabalho, selecione a pasta de trabalho, clique na seta para baixo que aparece à direita e, em seguida, selecione **gerenciar atualização de dados do PowerPivot**. Talvez seja necessário aguardar alguns minutos se o trabalho de atualização de dados estiver retornando um grande volume de dados.  
  
 Se ocorrer um erro, você poderá clicar **configurar agendamento** na atualização de dados a página de histórico para tentar outras credenciais. Talvez você também precise inspecionar as informações de conexão de fonte de dados na pasta de trabalho original para exibir a cadeia de conexão que é usada durante a atualização de dados. A cadeia de conexão oferecerá informações sobre o local do servidor e o banco de dados que pode ser usado para solucionar o problema.  
  
 Para obter mais informações sobre como solucionar problemas, consulte [Troubleshooting PowerPivot Data Refresh](https://go.microsoft.com/fwlink/p/?LinkID=223279) no Wiki do TechNet.  
  
##  <a name="config3rd"></a> Configurar uma conta predefinida para acessar fontes de dados externas ou de terceiros  
 Servidores de banco de dados costumam conter os próprios métodos de autenticação. Se você tiver uma pasta de trabalho do PowerPivot que exige credenciais de banco de dados para acessar uma fonte de dados externa durante a atualização de dados, poderá criar uma ID de aplicativo de destino para as credenciais e, depois, especificar o aplicativo de destino na seção Fontes de dados da página de atualização de dados programada.  
  
 Esta etapa somente será necessária se você quiser proporcionar aos usuários uma opção de substituir as credenciais de banco de dados que já estão inseridas na pasta de trabalho PowerPivot.  
  
 Esta etapa só funciona quando a cadeia de conexão já inclui um nome de usuário e uma senha. Note que a existência de credenciais na cadeia de conexão é relativamente incomum; portanto, sua capacidade de fazer uso desta opção é limitada. Na maioria dos casos, você terá apenas uma ID de usuário e uma senha na cadeia de conexão se estiver usando a autenticação de banco de dados para se conectar à fonte de dados. Para obter mais informações sobre como verificar a cadeia de caracteres de conexão para ver se ele inclui uma ID de usuário e senha, consulte a seção "Conceder permissões para criar agendas e acessar dados externos" [atualização de dados do PowerPivot com SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md).  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **proteger o serviço de Store**.  
  
3.  Em gerenciar aplicativos de destino, clique em **New**.  
  
4.  Em ID do aplicativo de destino, digite uma cadeia de texto. Ela deve ser exclusiva, mas também fácil de lembrar. Os usuários digitarão essa cadeia de caracteres nas páginas da agenda de atualização de dados sempre que desejarem usar as credenciais armazenadas nesse aplicativo.  
  
5.  Em Nome para Exibição, digite um nome descritivo. Esse nome é usado somente para fins de exibição. Ele não é usado para especificar o aplicativo de destino em uma agenda de atualização de dados.  
  
6.  Em Email de Contato, digite seu endereço de email.  
  
7.  Em tipo de aplicativo de destino, selecione **grupo**.  
  
8.  Ignore a URL da página do aplicativo de destino. A atualização de dados PowerPivot não usa essa URL.  
  
9. Clique em **Avançar**.  
  
10. No **especificam os campos de credenciais para o seu aplicativo de destino de Store seguro** página, aceite os valores padrão apenas se a fonte de dados usa a autenticação do Windows. Caso contrário, escolha os tipos de campo que são válidos para a sua fonte de dados e edite os nomes de campo para corresponder ao tipo.  
  
     Por exemplo, você pode especificar Nome de Usuário SQL Server e Senha de Usuário SQL Server para nomes de campos e, depois, escolher Nome de Usuário e Senha para tipos de campos.  
  
11. Clique em Avançar.  
  
12. Em Administradores de Aplicativo de Destino, especifique as contas de usuário de domínio do Windows de usuários do SharePoint que devem ter acesso administrativo às configurações de aplicativo.  
  
13. Em Membros, adicione as contas de usuário e grupo a seguir:  
  
    1.  Como você está criando o aplicativo, acrescente sua conta de usuário do Windows à lista de Membros.  
  
    2.  Adicione a identidade de pool de aplicativos de cada aplicativo de serviço PowerPivot que estará usando o aplicativo de destino para acessar suas credenciais armazenadas. Para exibir a identidade, vá para **gerenciar aplicativos de serviço**, selecione o aplicativo de serviço PowerPivot clicando no espaço vazio ao lado do nome (Isso seleciona a linha) e, em seguida, clique em **propriedades**. A conta de segurança que aparece nesta página é a conta que você deseja adicionar como um membro do aplicativo de destino.  
  
    3.  Adicione as contas de usuário e grupo do Windows que irão inserir esse aplicativo de destino na seção de fontes de dados de uma página de agenda de atualização de dados.  
  
14. Clique em **OK**.  
  
15. Selecione o aplicativo de destino que você acabou de criar, clique na seta para baixo e selecione **definir credenciais.**  
  
16. Digite as credenciais que serão usadas para se conectar à fonte de dados (por exemplo, o nome de usuário e a senha de um logon do SQL Server).  
  
17. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Atualização de dados PowerPivot com SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
