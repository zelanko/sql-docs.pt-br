---
title: "Salvar e Executar Pacote (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.saveschedule.f1"
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Salvar e Executar Pacote (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Depois de especificar e configurar sua fonte e destino de dados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Salvar e executar o pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da configuração, você também poderá salvar o pacote do SSIS ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente.
  
**O que é um pacote?** O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. No SSIS, a unidade básica é o pacote. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Captura de tela da página Salvar e Executar Pacote  
A captura de tela a seguir mostra a página **Salvar e Executar o Pacote** do assistente. 
   
![Save and run package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-and-run.png "Save and run package page of the Import and Export Wizard") 
  
## <a name="run-and-save-the-package"></a>Executar e salvar o pacote 
 Para continuar, você precisa selecionar pelo menos uma das duas opções a seguir.  
  
 **Executar imediatamente**  
 Selecione esta opção para executar o pacote imediatamente.  
  
 **Salvar Pacote SSIS**  
 Salve o pacote. Opcionalmente, você pode personalizar o pacote e executá-lo novamente posteriormente. Se você optar por salvar o pacote, haverá opções adicionais na próxima página, **Salvar pacote SSIS**. A opção para salvar o pacote estará disponível somente se você tiver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition ou uma edição superior instalada.   
  
> [!NOTE] Se você concluir o assistente, executar o pacote e interrompê-lo antes de a execução terminar, o pacote não será salvo mesmo se a caixa de seleção **Salvar** tiver sido marcada nesta página.  
  
## <a name="specify-options-for-saving-the-package"></a>Especificar opções para salvar o pacote
**SQL Server**  
 Selecione esta opção para salvar o pacote no banco de dados **msdb** na tabela **sysssispackages**.
 
> [!NOTE] Essa opção não salva o pacote no banco de dados do catálogo do SSIS (SSISDB).  

 Selecione o servidor de destino e forneça credenciais para se conectar ao servidor na próxima página, **Salvar pacote SSIS**. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Sistema de Arquivos**  
 Selecione essa opção para salvar o pacote como um arquivo com extensão **.dtsx**.  
  
 Selecione a pasta de destino e o nome de arquivo para o pacote na próxima página, **Salvar pacote SSIS**. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Especificar o nível de proteção do pacote
 **Nível de Proteção do Pacote**  
 Selecione um nível de proteção na lista para ajudar a proteger os dados no pacote.  
  
 O nível de proteção determina o método de proteção, a senha ou a chave de usuário, bem como o escopo de proteção do pacote. A proteção pode incluir todos os dados ou apenas os dados confidenciais. Para obter mais informações sobre as opções disponíveis, consulte [Controle de acesso para dados confidenciais em pacotes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 **Senha**  
 Digite uma senha.  
  
 **Digite a senha novamente**  
 Digite a senha novamente.  
  
> [!NOTE] As opções de senha só estarão disponíveis se você especificar a opção **Nível de proteção do pacote** como **Criptografar dados confidenciais com senhas** ou como **Criptografar todos os dados com senhas**.  

## <a name="can-i-run-and-save-the-package"></a>Posso executar e salvar o pacote?
 O método que você usa para iniciar o assistente determina se você pode executar e salvar o pacote criado pelo assistente. Em alguns casos, tanto a opção **Executar** quanto a opção **Salvar** estarão desabilitadas nesta página do assistente.
 
|Como iniciar o assistente|Você consegue executar o pacote?|Você consegue salvar o pacote?|
|------------------------|------------------------|-------------------------|
|Inicie o assistente no menu Iniciar, no prompt de comando ou no SQL Server Management Studio.|Você pode executar o pacote imediatamente no fim do assistente marcando a caixa de seleção **Executar imediatamente**. Por padrão, essa caixa de seleção é marcada e o pacote é executado imediatamente.|Se tiver o SQL Server Standard Edition ou superior instalado, você também poderá salvar o pacote.|
|Inicie o assistente de um projeto do Integration Services no SSDT (SQL Server Data Tools).|Não é possível executar o pacote antes de sair do assistente. Dessa forma, você poderá executar o pacote no SQL Server Data Tools.|O assistente salva o pacote no projeto do Integration Services do qual você iniciou o assistente.|

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Sobre as duas páginas de opções para salvar o pacote  
 A página **Salvar e executar pacote** é uma das duas páginas nas quais você pode selecionar opções para salvar o pacote do SSIS.  
  
-   Na página atual, escolha se você deseja salvar o pacote no SQL Server ou como um arquivo. Você também pode escolher as configurações de segurança para o pacote salvo.  
  
-   Em seguida, na página **Salvar pacote SSIS**, forneça um nome para o pacote e mais informações sobre onde salvá-lo. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Essas opções estarão disponíveis somente se você selecionar a opção **Salvar pacote SSIS** nesta página.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar se deseja executar a operação de cópia imediatamente e salvar o pacote, a próxima página dependerá das opções que você escolher.  
  
-   Se você tiver escolhido a opção para executar o pacote imediatamente, mas não para salvá-lo, a próxima página será **Concluir o assistente**. Nessa página, examine as escolhas feitas no assistente e inicie a operação de cópia. Para obter mais informações, consulte [Concluir o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Se você tiver selecionado a opção para salvar o pacote, a próxima página será **Salvar pacote SSIS**. Nessa página, você deve especificar as opções adicionais para salvar o pacote. (Depois de salvar o pacote, a página a seguinte será **Concluir o assistente**.) Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Consulte também  
[Salvar pacotes](../../integration-services/save-packages.md)  
[Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
  
