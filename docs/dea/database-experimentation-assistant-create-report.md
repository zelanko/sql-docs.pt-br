---
title: Criar relatórios de análise no Assistente de experimentação do banco de dados para atualizações do SQL Server
description: Criar relatórios de análise no Assistente para experimentos de banco de dados
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: ff0a31fc4d825966fefafc11d8780862634f1937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794480"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>Criar relatórios de análise no Assistente de experimentação do banco de dados

Depois que você repetir o rastreamento de origem em ambos os servidores de destino, você pode gerar um relatório de análise no banco de dados experimentação Assistant (DEA). Relatórios de análise de ajudarão-lo a obter informações sobre as implicações de desempenho das alterações propostas.

## <a name="create-an-analysis-report"></a>Criar um relatório de análise

No DEA, selecione o ícone de menu. No menu expandido, selecione **relatórios de análise de** ao lado do ícone de lista de verificação.

![Menu de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

Sob **relatórios de análise**, selecione **relatório de análise de novos**.

![Novo menu do relatório de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

Insira ou selecione as seguintes informações:

- **Nome do relatório**: Insira um nome para seu relatório. O nome do relatório é usado tanto para A e B bancos de dados. Exemplo: *A (ou B)* + *nome do relatório* + *identificador exclusivo*. 
- **Nome do servidor**: Insira o nome do computador servidor que você deseja incluir em A, B e bancos de dados de análise.
- **Nome da instância do SQL Server**: Insira o nome da instância do SQL Server a ser usado para o relatório.
- **Rastreamento de servidor de origem**: Insira o primeiro arquivo de rastreamento (. TRC) do SQL Server (2008 R2).
- **Rastreamento de servidor de destino**: Enter the target SQL Server (2014) first .trc file.

![Nova página de relatório de análise](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>Gerar um relatório

Depois de inserir ou selecionar as informações necessárias sobre o **novo relatório de análise** página, selecione **iniciar** para começar a criar o relatório. Se as informações inseridas for válidas, o relatório de análise é criado. Caso contrário, as caixas de texto que tem informações inválidas são realçadas com vermelho. Certifique-se de que você insira os valores corretos e, em seguida, selecione **iniciar**. 

Um novo relatório de análise é gerado. O banco de dados de análise segue o esquema de nomenclatura análise + *nome do relatório especificado pelo usuário* + *identificador exclusivo*.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Perguntas frequentes sobre relatórios de análise

### <a name="what-does-my-analysis-report-tell-me"></a>O que meu relatório de análise de dizer?
    
DEA usa testes estatísticos para analisar sua carga de trabalho e determinar como cada consulta foi executada de destino 1 para 2 de destino. Ele fornece detalhes de desempenho para cada consulta. Saiba mais sobre DEA na [começar](database-experimentation-assistant-get-started.md).
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>Posso criar um novo relatório de análise enquanto outro relatório está sendo gerado?
    
Não.  Atualmente, apenas um relatório pode ser gerado por vez para evitar conflitos. No entanto, você pode executar mais de uma captura e reprodução ao mesmo tempo.

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>Atualizei DEA para a versão 2.0. Posso ainda exibir e usar meus relatórios antigos?
    
Sim. Para exibir relatórios gerados anteriormente, você deve atualizar o esquema do relatório. Para obter mais informações, consulte [DEA 2.0: Atualizar o esquema de banco de dados para o relatório de análise no DEA](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/).
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>Pode gerar um relatório de análise usando o prompt de comando?
    
Sim. Você pode gerar um relatório de análise no prompt de comando. Em seguida, você pode exibir o relatório na interface do usuário. Para obter mais informações, consulte [executados no prompt de comando](database-experimentation-assistant-run-command-prompt.md).
    
## <a name="troubleshoot-analysis-reports"></a>Solucionar problemas de relatórios de análise

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>Quais permissões de segurança necessário gerar e exibir um relatório de análise no meu servidor?
    
O usuário que está conectado ao DEA deve ter direitos sysadmin no servidor de análise. Se o usuário faz parte de um grupo, verifique se que o grupo tem direitos de sysadmin.

|Possíveis erros|Solução|  
|---|---|  
|Não é possível conectar-se ao banco de dados. Verifique se que você tem direitos de sysadmin para analisar e exibir os relatórios.|Você pode não ter direitos de acesso ou sysadmin no servidor ou banco de dados. Confirmar seus direitos de logon e tente novamente.|  
|Não é possível gerar **nome do relatório** no servidor **nome do servidor**. Para obter detalhes, consulte o **nome do relatório** relatório.|Você não pode ter os direitos de sysadmin necessários para gerar um novo relatório. Para ver erros detalhados, selecione o relatório com erros e verifique os logs em % temp %\\DEA.|  
|O usuário atual não tem as permissões necessárias para executar a operação. Verifique se que você tem direitos de sysadmin para realizar o rastreamento e analisar os relatórios.|Você não tem os direitos de sysadmin necessários para gerar um novo relatório.|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>Não é possível conectar-se ao computador que executa o SQL Server
    
- Confirme se o nome do computador executando o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando o SQL Server Management Studio (SSMS).
- Confirme que a configuração do firewall não bloqueie conexões com o computador executando o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessário. 

Você pode ver mais detalhes nos logs em % temp %\\DEA. Se o problema persistir, entre em contato com a equipe de produto.

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>Eu vejo um erro quando posso gerar um relatório de análise
    
Acesso à Internet é necessário na primeira vez que você gerar um relatório de análise depois de instalar DEA. Acesso à Internet é necessário para baixar os pacotes que são necessários para análise estatística.

Se ocorrer um erro enquanto o relatório é criado, a página de progresso mostra a etapa específica em que falha na geração de análise. Você pode ver mais detalhes nos logs em % temp %\\DEA. Verifique se você tiver uma conexão válida para o servidor com as permissões necessárias e tente novamente. Se o problema persistir, entre em contato com a equipe de produto.

|Possíveis erros|Solução|  
|---|---|  
|RInterop encontrou um erro na inicialização. Verifique os logs de RInterop e tente novamente.|DEA requer acesso à internet para baixar os pacotes de R dependentes. Verifique os logs de RInterop em % temp %\\RInterop e DEA registra em log em % temp %\\DEA. Se RInterop foi inicializado incorretamente ou se ele inicializado sem os pacotes de R corretos, você poderá ver a exceção "Falha ao gerar o relatório de análise de novo" após a etapa InitializeRInterop nos logs de DEA.<br><br>Os logs de RInterop também podem mostrar um erro semelhante a "não há nenhum pacote jsonlite disponível." Se seu computador não tiver acesso à internet, você pode baixar manualmente o pacote necessário jsonlite R:<br><br><li>Vá para o % userprofile %\\DEARPackages pasta no sistema de arquivos do computador. Essa pasta consiste em pacotes usados pelo R para DEA.</li><br><li>Se a pasta jsonlite está ausente na lista de pacotes instalados, você precisa de uma máquina com acesso à internet para baixar a versão de lançamento do jsonlite\_1.4.zip partir [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html).</li><br><li>Copie o arquivo. zip para o computador no qual você está executando DEA.  Extraia a pasta jsonlite e copiá-lo para % userprofile %\\DEARPackages. Esta etapa instala automaticamente o pacote jsonlite em R. A pasta deve ser nomeada **jsonlite** e o conteúdo deve ser diretamente dentro da pasta, não um nível abaixo.</li><br><li>Fechar DEA, abra-a novamente e tente análise novamente.</li><br>Você também pode usar o RGUI. Vá para **pacotes** > **instalar do zip**. Vá para o pacote baixado anteriormente e instalar.<br><br>Se RInterop foi inicializado e configurado corretamente, você deverá ver "Instalando dependentes R pacote jsonlite" nos logs de RInterop.|  
|Não é possível conectar-se à instância do SQL Server, verifique se que o nome do servidor está correto e verificar o acesso necessário para o usuário que está conectado.|Você pode não ter acesso ou direitos de usuário para o servidor ou o nome do servidor podem estar incorretos.| 
|Processo RInterop atingiu o tempo limite. Verifique os logs DEA e RInterop, interromper o processo de RInterop no Gerenciador de tarefas e, em seguida, tente novamente.<br><br>ou em<br><br>RInterop está em estado de falha. Interromper o processo de RInterop no Gerenciador de tarefas e, em seguida, tente novamente.|Verifique os logs em % temp %\\RInterop para confirmar o erro. Remova o processo de RInterop no Gerenciador de tarefas antes de tentar novamente. Se o problema persistir, entre em contato com a equipe de produto.| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>O relatório é gerado, mas dados parecem estar ausente
    
Verifique o banco de dados no computador de análise que está executando o SQL Server para confirmar a existem de dados. Verifique se o banco de dados de análise existe e verificar suas tabelas. Por exemplo, confira essas tabelas: TblBatchesA, TblBatchesB e TblSummaryStats.

Se os dados não existirem, os dados talvez não tenha sido copiado corretamente ou o banco de dados pode estar corrompido. Se apenas alguns dados estão ausentes, os arquivos de rastreamento criado na captura ou reprodução talvez não capturou sua carga de trabalho com precisão. Se os dados estiverem lá, verifique os arquivos de log em % temp %\\DEA para ver se os erros foram registrados. Em seguida, tente novamente gerar o relatório de análise.

Mais perguntas ou comentários? Envie comentários por meio da ferramenta DEA, escolhendo o ícone de smiley no canto inferior esquerdo.  

## <a name="next-steps"></a>Próximas etapas

- Para saber como exibir o relatório de análise, consulte [exibir relatórios](database-experimentation-assistant-view-report.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
