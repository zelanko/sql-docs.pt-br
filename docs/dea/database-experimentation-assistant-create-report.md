---
title: Criar relatórios de análise
description: Criar relatórios de análise no Assistente para Experimentos de Banco de Dados
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 4d3f057ffcfb1030b473b69f96b7204b3a975613
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74307970"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>Criar relatórios de análise no Assistente para Experimentos de Banco de Dados (SQL Server)

Depois de reproduzir o rastreamento de origem nos dois servidores de destino, você poderá gerar um relatório de análise no Assistente para Experimentos de Banco de Dados (DEA). Os relatórios de análise ajudam você a obter informações sobre as implicações de desempenho das alterações propostas.

## <a name="create-an-analysis-report"></a>Criar um relatório de análise

Em DEA, selecione o ícone de menu. No menu expandido, selecione **relatórios de análise** ao lado do ícone lista de verificação.

![Menu de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

Em **relatórios de análise**, selecione **novo relatório de análise**.

![Menu novo relatório de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

Insira ou selecione as seguintes informações:

- **Nome do relatório**: Insira um nome para o relatório. O nome do relatório é usado para bancos de dados A e B. Exemplo: um*identificador exclusivo*do*nome* +  *do relatório (ou B)* + .
- **Nome do servidor**: Insira o nome do computador do servidor que você deseja incluir nos bancos de dados de análise a, B e.
- **Nome da instância do SQL Server**: Insira o nome da instância de SQL Server a ser usada para o relatório.
- **Rastreamento do servidor de origem**: insira o SQL Server (2008 R2) primeiro arquivo de rastreamento (. trc).
- **Rastreamento do servidor de destino**: insira o SQL Server de destino (2014) primeiro arquivo. trc.

![Página novo relatório de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>Gerar um relatório

Depois de inserir ou selecionar as informações necessárias na página **novo relatório de análise** , selecione **Iniciar** para começar a criar o relatório. Se as informações inseridas forem válidas, o relatório de análise será criado. Caso contrário, as caixas de texto com informações inválidas serão realçadas com vermelho. Certifique-se de inserir os valores corretos e, em seguida, selecione **Iniciar**.

Um novo relatório de análise é gerado. O banco de dados de análise segue a análise do esquema de nomenclatura + +  *nome de relatório especificado pelo usuário**identificador exclusivo*.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Perguntas frequentes sobre relatórios de análise

**P: o que meu relatório de análise me informa?**

O DEA usa testes estatísticos para analisar sua carga de trabalho e determinar como cada consulta foi executada do destino 1 para o destino 2. Ele fornece detalhes de desempenho para cada consulta. Saiba mais sobre o DEA em [introdução](database-experimentation-assistant-get-started.md).

**P: posso criar um novo relatório de análise enquanto outro relatório está sendo gerado?**

Não.  Atualmente, apenas um relatório pode ser gerado por vez para evitar conflitos. No entanto, você pode executar mais de uma captura e reprodução ao mesmo tempo.

**P: atualizei o DEA para a versão 2,0. Ainda posso exibir e usar meus relatórios antigos?**

Sim. Para exibir relatórios gerados anteriormente, você deve atualizar o esquema do relatório. Para obter mais informações, consulte [DEA 2,0: atualizar o esquema de banco de dados para o relatório de análise no DEA](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/).

**P: posso gerar um relatório de análise usando o prompt de comando?**

Sim. Você pode gerar um relatório de análise no prompt de comando. Em seguida, você pode exibir o relatório na interface do usuário. Para obter mais informações, consulte [executar no prompt de comando](database-experimentation-assistant-run-command-prompt.md).

## <a name="troubleshoot-analysis-reports"></a>Solucionar problemas de relatórios de análise

**P: quais permissões de segurança preciso para gerar e exibir um relatório de análise no meu servidor?**

O usuário que fez logon no DEA deve ter direitos de sysadmin no Analysis Server. Se o usuário fizer parte de um grupo, verifique se o grupo tem direitos sysadmin.

|Possíveis erros|Solução|  
|---|---|  
|Não é possível conectar-se ao banco de dados. Verifique se você tem direitos de sysadmin para analisar e exibir os relatórios.|Talvez você não tenha direitos de acesso ou sysadmin para o servidor ou banco de dados. Confirme seus direitos de logon e tente novamente.|  
|Não é possível gerar o **nome do relatório** no **nome do servidor**do servidor. Para obter detalhes, verifique o relatório **nome do relatório** .|Talvez você não tenha os direitos sysadmin necessários para gerar um novo relatório. Para ver os erros detalhados, selecione o relatório com erros e verifique os logs em% temp%\\DEA.|  
|O usuário atual não tem as permissões necessárias para executar a operação. Verifique se você tem direitos de sysadmin para executar o rastreamento e analisar os relatórios.|Você não tem os direitos sysadmin necessários para gerar um novo relatório.|  

**P: não consigo me conectar ao computador que executa o SQL Server**

- Confirme se o nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando SQL Server Management Studio (SSMS).
- Confirme se a configuração do firewall não bloqueia conexões com o computador que executa o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessários.

Você pode ver mais detalhes nos logs em% temp%\\DEA. Se o problema persistir, entre em contato com a equipe do produto.

**P: vejo um erro ao gerar um relatório de análise**

O acesso à Internet é necessário na primeira vez que você gera um relatório de análise após a instalação do DEA. O acesso à Internet é necessário para baixar pacotes que são necessários para análise estatística.

Se ocorrer um erro enquanto o relatório é criado, a página progresso mostra a etapa específica em que a geração da análise falhou. Você pode ver mais detalhes nos logs em% temp%\\DEA. Verifique se você tem uma conexão válida com o servidor com os direitos de usuário necessários e tente novamente. Se o problema persistir, entre em contato com a equipe do produto.

|Possíveis erros|Solução|  
|---|---|  
|RInterop encontrou um erro na inicialização. Verifique os logs do RInterop e tente novamente.|O DEA requer acesso à Internet para baixar pacotes R dependentes. Verifique os logs do RInterop nos logs\\% Temp% RINTEROP e DEA em%\\Temp% DEA. Se o RInterop foi inicializado incorretamente ou se ele foi inicializado sem os pacotes de R corretos, você poderá ver a exceção "falha ao gerar o novo relatório de análise" após a etapa InitializeRInterop nos logs do DEA.<br><br>Os logs do RInterop também podem mostrar um erro semelhante a "não há um pacote jsonlite disponível". Se seu computador não tiver acesso à Internet, você poderá baixar manualmente o pacote jsonlite R necessário:<br><br><li>Vá para a pasta% UserProfile\\% DEARPackages no sistema de arquivos da máquina. Essa pasta consiste nos pacotes usados pelo R para DEA.</li><br><li>Se a pasta jsonlite estiver ausente na lista de pacotes instalados, você precisará de um computador com acesso à Internet para baixar a versão de\_lançamento do jsonlite 1.4 [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html). zip de.</li><br><li>Copie o arquivo. zip para o computador em que você está executando o DEA.  Extraia a pasta jsonlite e copie-a para%\\USERPROFILE% DEARPackages. Essa etapa instala automaticamente o pacote jsonlite em R. A pasta deve ser nomeada **jsonlite** e o conteúdo deve estar diretamente dentro da pasta, não um nível abaixo.</li><br><li>Feche DEA, reabra e tente novamente a análise.</li><br>Você também pode usar o RGUI. Vá para **pacotes** > **instalar do zip**. Vá para o pacote que você baixou anteriormente e instale o.<br><br>Se o RInterop foi inicializado e configurado corretamente, você deverá ver "Instalando o pacote R dependente jsonlite" nos logs do RInterop.|  
|Não é possível conectar-se à instância de SQL Server, verifique se o nome do servidor está correto e verifique o acesso necessário ao usuário que está conectado.|Talvez você não tenha direitos de acesso ou de usuário no servidor, ou o nome do servidor pode estar incorreto.|
|O processo de RInterop atingiu o tempo limite. Verifique os logs de DEA e RInterop, interrompa o processo de RInterop no Gerenciador de tarefas e tente novamente.<br><br>ou<br><br>RInterop está em estado com falha. Pare o processo RInterop no Gerenciador de tarefas e tente novamente.|Verifique os logs em% temp\\% RInterop para confirmar o erro. Remova o processo RInterop do Gerenciador de tarefas antes de tentar novamente. Entre em contato com a equipe do produto se o problema persistir.|

**P: o relatório é gerado, mas os dados parecem estar ausentes**

Verifique o banco de dados no computador de análise que está executando SQL Server para confirmar a existência dos mesmos. Verifique se o banco de dados de análise existe e verifique suas tabelas. Por exemplo, verifique estas tabelas: TblBatchesA, TblBatchesB e TblSummaryStats.

Se os dados não existirem, os dados poderão não ter sido copiados corretamente ou o banco de dado poderá estar corrompido. Se apenas alguns dados estiverem ausentes, os arquivos de rastreamento criados na captura ou reprodução poderão não ter capturado a carga de trabalho com precisão. Se os dados estiverem lá, verifique os arquivos de log em% temp\\% DEA para ver se algum erro foi registrado. Em seguida, tente gerar novamente o relatório de análise.

Mais perguntas ou comentários? Envie comentários por meio da ferramenta DEA escolhendo o ícone de Smiley no canto inferior esquerdo. 

## <a name="see-also"></a>Consulte também

- Para saber como exibir o relatório de análise, consulte [exibir relatórios](database-experimentation-assistant-view-report.md).
