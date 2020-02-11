---
title: Configurar a conta de atualização de dados autônoma do PowerPivot (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 894e7d4fb5a0234643cf237e767a8ae999e67496
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087417"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>Configurar a conta autônoma de atualização de dados PowerPivot (PowerPivot para SharePoint)
  A conta autônoma de atualização de dados PowerPivot é uma conta designada para executar trabalhos de atualização de dados PowerPivot em um farm do SharePoint. Ao configurá-lo, você habilita a opção **usar a conta de atualização de dados configurada pelo administrador** em uma página de agendamento de atualização de dados (veja abaixo). Autores de pasta de trabalho que agendarem a atualização de dados poderão escolher essa opção se quiserem usar a conta autônoma de atualização de dados PowerPivot para executar um trabalho de atualização de dados. Para obter mais informações sobre como exibir as opções de credenciais em uma agenda de atualização de dados, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 Dependendo de quais opções que você selecionou ao configurar o servidor, a conta autônoma de atualização de dados já poderá ter sido criada. Em uma configuração padrão, a identidade da conta autônoma de atualização de dados é inicialmente definida como a conta de farm. Você pode melhorar a segurança de sua implantação alterando a conta para ser executada como um usuário diferente. Siga estas instruções para alterar a conta: [atualizar as credenciais usadas por uma conta de atualização de dados autônoma do PowerPivot existente](#bkmk_editUA).  
  
 Para ver todos os outros cenários de instalação, configure a conta manualmente usando as instruções a seguir.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisitos](#bkmk_prereq)  
  
 [Etapa 1: Criar um aplicativo de destino e definir as credenciais](#bkmk_create)  
  
 [Etapa 2: Especificar a conta autônoma nas páginas de configuração do servidor do PowerPivot](#bkmk_specifyUA)  
  
 [Etapa 3: conceder permissões de colaboração para a conta](#bkmk_grant)  
  
 [Etapa 4: conceder permissões de leitura para acessar fontes de dados externas usadas na atualização de dados](#bkmk_dbread)  
  
 [Etapa 5: Verifique a disponibilidade da conta em páginas de configuração de atualização de dados](#bkmk_verify)  
  
 [Usando a conta autônoma de atualização de dados PowerPivot.](#bkmk_use)  
  
 [Atualizar as credenciais usadas por uma conta existente de atualização de dados autônoma do PowerPivot](#bkmk_editUA)  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 O Serviço de Repositório Seguro deve estar habilitado e configurado, e uma chave mestra deve ser gerada. Para obter instruções sobre como fazer isso, consulte [atualização de dados PowerPivot com o SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 Você deve decidir com antecedência qual conta de usuário do domínio Windows usar como a conta autônoma de atualização de dados PowerPivot. Essa deve ser uma conta especificamente criada para essa finalidade, para que você possa monitorar como ela é usada.  
  
 Você deve conhecer a identidade do aplicativo do Serviço do Sistema PowerPivot. Você dará a essa conta de serviço permissões de **controle total** sobre a conta de atualização de dados autônoma quando criar o aplicativo de destino para ele na etapa 1. Essas permissões permitem que o Serviço do Sistema PowerPivot recupere as credenciais da conta de atualização de dados autônoma durante a atualização de dados. Para obter as informações necessárias da conta de serviço, abra a página **Configurar contas de serviço** na administração central e selecione o pool de aplicativos de serviço usado pelo aplicativo de serviço PowerPivot. Por padrão, esse é o **pool de aplicativos de serviço – o sistema de serviços Web do SharePoint**.  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>Configurar a conta autônoma de atualização de dados PowerPivot  
 Você pode configurar somente uma conta autônoma de atualização de dados PowerPivot para cada aplicativo de serviço PowerPivot. As informações de conta são armazenadas no Serviço de Repositório Seguro em um aplicativo de destino que esteja definido como uma conta de usuário do domínio Windows predefinida. Quando o aplicativo de destino é criado, você pode especificá-lo como a conta de atualização de dados PowerPivot nas páginas de configuração de um aplicativo de serviço PowerPivot.  
  
> [!NOTE]  
>  Quando a atualização de dados é executada com a conta autônoma de atualização de dados, o relatório de uso e o histórico de atualização de dados são registrados na conta de usuário Windows usada para atualização de dados autônoma. Se você precisar de um registro mais exato das pessoas que estão solicitando atualização de dados ou que possuem agendas, considere um das outras opções para executar a atualização de dados. Ou seja, fazer com que os usuários especifiquem as próprias credenciais (esse é o padrão) ou criar aplicativos de destino adicionais para armazenar credenciais do Windows que você queira usar para fins de atualização de dados. Para obter mais informações, consulte [configurar credenciais armazenadas para a atualização de dados PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 A criação da conta de atualização de dados autônoma se divide em cinco partes.  
  
-   Criar um aplicativo de destino no Serviço de Repositório Seguro para a conta e especificar as credenciais.  
  
-   Especificar a ID do aplicativo de destino para a conta autônoma de atualização de dados na página de configuração do servidor PowerPivot.  
  
-   Conceder permissões de colaboração à conta.  
  
-   Conceder as permissões de leitura da conta para acessar fontes de dados externas durante atualização de dados.  
  
-   Verificar se a conta está disponível na página de agenda Gerenciar Atualização de Dados para uma pasta de trabalho PowerPivot publicada.  
  
###  <a name="bkmk_create"></a>Etapa 1: criar um aplicativo de destino e definir as credenciais  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **serviço de repositório seguro**.  
  
3.  Em gerenciar aplicativos de destino, clique em **novo**.  
  
4.  Em ID do aplicativo de destino, digite **PowerPivotDataRefresh**.  
  
5.  Em nome de exibição, digite **atualização de dados PowerPivot**.  
  
6.  Em Email de Contato, digite seu endereço de email.  
  
7.  Em tipo de aplicativo de destino, selecione **individual**.  
  
    > [!NOTE]  
    >  A especificação de um tipo de conta Individual é correta para este cenário porque apenas o aplicativo de serviço PowerPivot solicitará as credenciais da conta autônoma de atualização de dados PowerPivot. Na prática, o aplicativo de serviço é o único usuário da conta autônoma de atualização de dados, tornando o tipo de conta Individual a melhor opção para este aplicativo de destino.  
  
8.  Ignore a URL da página do aplicativo de destino. A atualização de dados PowerPivot não usa essa URL.  
  
9. Clique em **Próximo**.  
  
10. Na página **especificar os campos de credenciais para seu aplicativo de destino de repositório seguro** , aceite os valores padrão. Os nomes e tipos de campo devem ser Nome de Usuário do Windows e Senha do Windows  
  
11. Clique em **Próximo**.  
  
12. Em Administradores de Aplicativos de Destino, especifique a identidade do pool de aplicativos do aplicativo de serviço PowerPivot. O serviço requer permissões de **controle total** para que possa recuperar informações de conta de atualização de dados autônoma em tempo de execução. Além disso, especifique as contas de usuário de domínio do Windows de qualquer outro usuário do SharePoint que precise ter acesso administrativo às configurações do aplicativo.  
  
13. Clique em **OK**.  
  
14. Selecione o aplicativo de destino que você acabou de criar, clique na seta para baixo e selecione **definir credenciais.**  
  
15. Em **proprietários de credenciais**, digite uma conta de usuário de domínio do Windows para a qual você deseja ter permissões para atualizar as credenciais. As credenciais são usadas para ações de atualização de dados e os **proprietários de credenciais** têm permissões para modificar as credenciais.  
  
16. Clique em **OK**.  
  
###  <a name="bkmk_specifyUA"></a>Etapa 2: especificar a conta autônoma nas páginas de configuração do servidor PowerPivot  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Localize o aplicativo do Serviço PowerPivot. Você pode identificar um aplicativo de serviço por seu tipo. Um tipo de aplicativo de serviço PowerPivot é **Aplicativo de Serviço PowerPivot**.  
  
3.  Clique no nome do aplicativo de serviço PowerPivot. Aguarde a exibição do Painel de Gerenciamento PowerPivot.  
  
4.  Em ações, no canto superior direito, clique em **definir configurações do aplicativo de serviço**.  
  
5.  Em atualização de dados, na conta de atualização de dados autônoma PowerPivot, digite a ID do aplicativo de destino que você criou em uma etapa anterior: **PowerPivotDataRefresh**.  
  
6.  Clique em **OK**.  
  
###  <a name="bkmk_grant"></a>Etapa 3: conceder permissões de colaboração para a conta  
 Para que você possa usar a conta autônoma de atualização de dados PowerPivot, ela deve ter permissões de colaboração em qualquer pasta de trabalho PowerPivot para a qual é usada. Esse nível de permissão é necessário para abrir a pasta de trabalho de uma biblioteca e, em seguida, salvá-la novamente na biblioteca após os dados serem atualizados.  
  
 Atribuir permissões é uma etapa executada pelo administrador da coleção de sites. Podem ser atribuídas permissões do SharePoint na coleção de sites raiz ou em qualquer nível abaixo desse, inclusive em documentos e itens individuais. A forma como você define permissões irá variar dependendo do quanto elas precisam ser granulares. As etapas a seguir mostram uma abordagem para conceder permissões.  
  
1.  Em um site do SharePoint, em ações do site, clique em **permissões do site**.  
  
2.  Clique em **Conceder Permissões**.  
  
3.  Em Selecionar usuários, digite o nome da conta de usuário do domínio Windows que você designou como a conta autônoma do PowerPivot. Esse é o nome da conta de usuário do domínio Windows que você especificou no aplicativo de destino em Serviço de Repositório Seguro.  
  
4.  Em conceder permissões, selecione **conceder aos usuários a permissão diretamente**.  
  
5.  Selecione **Contribute**e clique em **OK**.  
  
###  <a name="bkmk_dbread"></a>Etapa 4: conceder permissões de leitura para acessar fontes de dados externas usadas na atualização de dados  
 Ao importar dados para uma pasta de trabalho PowerPivot, as conexões com dados externos são frequentemente baseadas em conexões confiáveis ou em conexões representadas que usam a identidade do usuário atual para conectar-se à fonte de dados. Estes tipos de conexões funcionam apenas quando o usuário atual tem permissão para ler os dados que está importando.  
  
 Em um cenário de atualização de dados, a mesma cadeia de conexão que foi usada para importar os dados é agora reutilizada para atualizar os dados. Se a cadeia de conexão assumir o usuário atual (por exemplo, uma cadeia de caracteres que inclua Integrated_Security=SSPI), o Serviço do Sistema PowerPivot passará a identidade do usuário da conta de atualização de dados autônoma do PowerPivot como o usuário atual. Essa conexão terá êxito apenas se a conta de atualização de dados autônoma do PowerPivot tiver permissões de leitura na fonte de dados externa.  
  
 Por isso, você deve conceder à conta autônoma de atualização de dados PowerPivot permissões somente leitura em todas as fontes de dados externas que são usadas em qualquer operação de atualização de dados executada na conta autônoma.  
  
 Se você for administrador das fontes de dados usadas em sua organização, poderá criar um logon e atribuir as permissões necessárias. Caso contrário, você deverá entrar em contato com os proprietários dos dados e fornecer as informações da conta. Especifique a conta de usuário do domínio Windows que mapeia para a conta de atualização de dados autônoma do PowerPivot. Essa é a conta que você especificou em "(etapa 1): criar um aplicativo de destino e definir as credenciais" neste tópico.  
  
###  <a name="bkmk_verify"></a>Etapa 5: verificar a disponibilidade da conta nas páginas de configuração de atualização de dados  
  
1.  Abra uma página de configuração de atualização de dados para uma pasta de trabalho publicada que contém dados do PowerPivot. Para obter instruções sobre como abrir a página, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
2.  Verifique se a opção **usar a conta de atualização de dados configurada pelo administrador** está habilitada na página configuração de atualização de dados.  
  
3.  Marque a caixa de seleção **também atualizar assim que possível** e clique em **OK**.  
  
4.  Na biblioteca que contém a pasta de trabalho, selecione a pasta de trabalho, clique na seta para baixo que aparece à direita e selecione **gerenciar atualização de dados PowerPivot**. Talvez seja necessário aguardar alguns minutos se o trabalho de atualização de dados estiver retornando um grande volume de dados.  
  
 Se ocorrer um erro, você poderá clicar em **Configurar agendamento** na página Histórico de atualização de dados para experimentar credenciais diferentes. Talvez você também precise inspecionar as informações de conexão de fonte de dados na pasta de trabalho original para exibir a cadeia de conexão que é usada durante a atualização de dados. A cadeia de conexão oferecerá informações sobre o local do servidor e o banco de dados que pode ser usado para solucionar o problema.  
  
 Para obter mais informações sobre solução de problemas, consulte [solução de problemas de atualização de dados PowerPivot](https://go.microsoft.com/fwlink/p/?LinkID=223279) no wiki do TechNet.  
  
##  <a name="bkmk_use"></a>Usando a conta autônoma de atualização de dados PowerPivot  
 Entre as três opções de credenciais na página de agendamento de atualização de dados PowerPivot, apenas a primeira corresponde à conta autônoma de atualização de dados. Selecione essa opção ao configurar a agenda de atualização de dados.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 Não use a terceira opção de credencial (aquela que exige que você informe a ID do aplicativo de destino) para acessar a conta autônoma de atualização de dados PowerPivot. Há uma verificação de representação adicional que é executada com essa opção que resultará em um erro de validação se você tentar usá-la com a conta autônoma de atualização de dados PowerPivot (ou qualquer aplicativo de destino baseado no tipo de conta Individual). Para obter mais informações sobre como usar a terceira opção, consulte [configurar credenciais armazenadas para a atualização de dados PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_editUA"></a>Atualizar as credenciais usadas por uma conta de atualização de dados autônoma PowerPivot existente  
 Se a conta autônoma de atualização de dados já estiver configurada pela instalação ou por um administrador, você poderá atualizar o nome do usuário ou a senha editando o aplicativo de destino que armazena as credenciais. Note que a identidade original do Windows que foi associada antes à conta autônoma de atualização de dados PowerPivot não ficará visível quando você editar as credenciais no Serviço de Repositório Seguro. Esteja você atualizando uma senha expirada ou especificando outra conta, sempre digite novamente o nome de usuário e a senha para esse aplicativo de destino no Serviço de Repositório Seguro.  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **serviço de repositório seguro**.  
  
3.  Marque a caixa de seleção ao lado de **PowerPivotDataRefresh**.  
  
4.  Em credenciais, clique em **definir**.  
  
5.  Em **proprietários de credenciais**, digite uma conta de usuário de domínio do Windows para a qual você deseja ter permissões para atualizar as credenciais. As credenciais são usadas para ações de atualização de dados e os **proprietários de credenciais** têm permissões para modificar as credenciais.  
  
6.  Em Nome do Usuário, digite a conta de usuário de domínio do Windows que fará parte das credenciais autônomas de atualização de dados.  
  
7.  Em Senha, digite a senha da conta e digite-a novamente para confirmá-la.  
  
8.  Clique em **OK**.  
  
 Se estiver alterando não apenas a senha, mas também o nome de usuário da conta, é bem provável que precise executar etapas de configuração adicionais, como conceder permissões de leitura a fontes de dados externas e permissões SharePoint para atualizar a pasta de trabalho PowerPivot. Para obter instruções, vá para esta etapa na configuração da conta de atualização de dados autônoma do PowerPivot: [etapa 3: conceder permissões de colaboração à conta](#bkmk_grant)e continue com todas as etapas restantes, concluindo com a verificação de que a conta está configurada corretamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualização de dados PowerPivot com o SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Atualização de dados PowerPivot](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
