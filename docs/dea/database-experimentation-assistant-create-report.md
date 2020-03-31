---
title: Criar relatórios de análise
description: Criar relatórios de análise no assistente de experimentação de banco de dados
ms.date: 01/24/2020
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
ms.openlocfilehash: f82aba87632abea4ac5fbc8b54daa6dfd0eb5b4a
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289834"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>Criar relatórios de análise no Database Experimentation Assistant (SQL Server)

Depois de reproduzir o rastreamento de origem em ambos os servidores de destino, você pode gerar um relatório de análise no DeA (Database Experimentation Assistant, assistente de experimentação de banco de dados). Os relatórios de análise ajudam você a obter insights sobre as implicações de desempenho das mudanças propostas.

## <a name="create-an-analysis-report"></a>Crie um relatório de análise

1. No DEA, selecione o ícone da lista, especifique o nome do servidor e o tipo de autenticação, selecione ou desmarque as caixas **de seleção de transcrição** e **o certificado do servidor Trust,** conforme apropriado para o seu cenário, e selecione **Conectar**.

   ![Conecte-se ao servidor com arquivos de rastreamento](./media/database-experimentation-assistant-create-report/dea-connect-to-server-with-trace-files.png)

2. Na tela **Relatórios de análise,** selecione **Novo relatório de análise**.

   ![Criar novo relatório de análise](./media/database-experimentation-assistant-create-report/dea-create-an-analysis-report.png)

3. Na tela **do relatório de análise Nova,** especifique um nome para o relatório, o local de armazenamento e o caminho para os arquivos de rastreamento Alvo 1 e Target 2 e, em seguida, selecione **Iniciar**.

   ![Especificar novos detalhes do relatório de análise](./media/database-experimentation-assistant-create-report/dea-new-analysis-report-details.png)

   Se as informações inseridas forem válidas, o relatório de análise será criado.

   ![Relatório de análise recém-criado](./media/database-experimentation-assistant-create-report/dea-newly-created-analysis-report.png)

      > [!NOTE]
      > Se alguma das informações inseridas for inválida, as caixas de texto que contenham as informações incorretas serão destacadas em vermelho. Faça as correções necessárias e selecione **Iniciar** novamente.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Perguntas frequentes sobre relatórios de análise

**P: O que meu relatório de análise me diz?**

O DEA usa testes estatísticos para analisar sua carga de trabalho e determinar como cada consulta foi aplicada do Alvo 1 para o Alvo 2. Ele fornece detalhes de desempenho para cada consulta. Saiba mais sobre o DEA em [Get started](database-experimentation-assistant-get-started.md).

**P: Posso criar um novo relatório de análise enquanto outro relatório está sendo gerado?**

Não.  Atualmente, apenas um relatório pode ser gerado por vez para evitar conflitos. No entanto, você pode executar mais de uma captura e replay ao mesmo tempo.

**P: Posso gerar um relatório de análise usando o prompt de comando?**

Sim. Você pode gerar um relatório de análise no prompt de comando. Em seguida, você pode ver o relatório na UI. Para obter mais informações, consulte [Executar no prompt de comando](database-experimentation-assistant-run-command-prompt.md).

## <a name="troubleshoot-analysis-reports"></a>Relatórios de análise de solução de problemas

**P: Quais permissões de segurança preciso gerar e visualizar um relatório de análise no meu servidor?**

O usuário que está logado no DEA deve ter direitos de sysadmin no servidor de análise. Se o usuário faz parte de um grupo, certifique-se de que o grupo tenha direitos de sysadmin.

|Possíveis erros|Solução|  
|---|---|  
|Não é possível se conectar ao banco de dados. Certifique-se de ter direitos de sysadmin para analisar e visualizar os relatórios.|Você pode não ter acesso ou direitos sysadmin para o servidor ou banco de dados. Confirme seus direitos de login e tente novamente.|  
|Não é possível gerar **o nome do relatório** no nome do **servidor**. Para obter detalhes, consulte o relatório **nome do relatório.**|Você pode não ter os direitos de sysadmin necessários para gerar um novo relatório. Para ver erros detalhados, selecione o relatório de erro e\\verifique os logs em %temp% DEA.|  
|O usuário atual não tem as permissões necessárias para executar a operação. Certifique-se de ter direitos de sysadmin para realizar rastreamento e analisar os relatórios.|Você não tem os direitos de sysadmin necessários para gerar um novo relatório.|  

**Q: Eu não posso me conectar ao computador executando SQL Server**

- Confirme se o nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando o SQL Server Management Studio (SSMS).
- Confirme se a configuração do firewall não bloqueia as conexões com o computador executando o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessários.

Você pode ver mais detalhes nos logs em %temp%\\DEA. Se o problema persistir, entre em contato com a equipe do produto.

**P: Eu vejo um erro quando eu gero um relatório de análise**

O acesso à Internet é necessário na primeira vez que você gera um relatório de análise após a instalação do DEA. O acesso à Internet é necessário para baixar pacotes que são necessários para análise estatística.

Se ocorrer um erro enquanto o relatório é criado, a página progresso mostrará a etapa específica em que a geração de análise falhou. Você pode ver mais detalhes nos logs em %temp%\\DEA. Verifique se você tem uma conexão válida com o servidor com os direitos de usuário necessários e, em seguida, tente novamente. Se o problema persistir, entre em contato com a equipe do produto.

|Possíveis erros|Solução|  
|---|---|  
|RInterop acertou um erro na inicialização. Verifique os registros do RInterop e tente novamente.|O DEA requer acesso à internet para baixar pacotes R dependentes. Verifique os logs RInterop\\em %temp% RInterop e\\DEA logs in %temp% DEA. Se o RInterop foi inicializado incorretamente ou se ele inicializou sem os pacotes R corretos, você poderá ver a exceção "Falha ao gerar novo relatório de análise" após a etapa InitializeRInterop nos logs DEA.<br><br>Os registros do RInterop também podem mostrar um erro semelhante ao "não há nenhum pacote jsonlite disponível". Se sua máquina não tiver acesso à internet, você pode baixar manualmente o pacote jsonlite R necessário:<br><br><li>Vá para a pasta\\%userprofile% DEARPackages no sistema de arquivos da máquina. Esta pasta consiste nos pacotes usados por R para DEA.</li><br><li>Se a pasta jsonlite estiver faltando na lista de pacotes instalados, você precisa de\_uma máquina com [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html)acesso à internet para baixar a versão de lançamento do jsonlite 1.4.zip de .</li><br><li>Copie o arquivo .zip para a máquina onde você está executando o DEA.  Extrair a pasta jsonlite e copiá-la para %userprofile%\\DEARPackages. Esta etapa instala automaticamente o pacote jsonlite em R. A pasta deve ser nomeada **jsonlite** e o conteúdo deve estar diretamente dentro da pasta, não um nível abaixo.</li><br><li>Feche a DEA, reabra e tente analisar novamente.</li><br>Você também pode usar o RGUI. Vá para **os pacotes instalados** > **a partir do zip**. Vá para o pacote que você baixou anteriormente e instale.<br><br>Se o RInterop foi inicializado e configurado corretamente, você deve ver "Instalando jsonlite de pacote R dependente" nos logs RInterop.|  
|Não é possível se conectar à instância do SQL Server, certifique-se de que o nome do servidor está correto e verifique o acesso necessário para o usuário que está logado.|Você pode não ter acesso ou direitos de usuário para o servidor, ou o nome do servidor pode estar incorreto.|
|Processo RInterop cronometrado. Verifique os registros DEA e RInterop, interrompa o processo RInterop no Gerenciador de tarefas e tente novamente.<br><br>ou<br><br>RInterop está em estado de falha. Pare o processo RInterop no Gerenciador de tarefas e tente novamente.|Verifique os logins em\\%temp% RInterop para confirmar o erro. Remova o processo RInterop do Gerenciador de tarefas antes de tentar novamente. Entre em contato com a equipe do produto se o problema persistir.|

**Q: O relatório é gerado, mas os dados parecem estar faltando**

Verifique o banco de dados no computador de análise que está executando o SQL Server para confirmar que os dados existem. Verifique se o banco de dados de análise existe e verifique suas tabelas. Por exemplo, verifique estas tabelas: TblBatchesA, TblBatchesB e TblSummaryStats.

Se os dados não existirem, os dados podem não ter sido copiados corretamente ou o banco de dados pode estar corrompido. Se apenas alguns dados estão faltando, os arquivos de rastreamento criados na captura ou replay podem não ter capturado sua carga de trabalho com precisão. Se os dados estão lá, verifique os\\arquivos de log em %temp% DEA para ver se algum erro foi registrado. Então, tente novamente gerar o relatório de análise.

Mais perguntas ou comentários? Envie comentários através da ferramenta DEA escolhendo o ícone sorridente no canto inferior esquerdo.

## <a name="see-also"></a>Confira também

- Para saber como visualizar o relatório de análise, consulte [Exibir relatórios](database-experimentation-assistant-view-report.md).
