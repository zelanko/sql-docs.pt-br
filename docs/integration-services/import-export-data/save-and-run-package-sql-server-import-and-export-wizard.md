---
title: "Salvar e executar pacote (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 40b8677cddf363e8789a2fc15b1c2aab5f49f58c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Salvar e Executar Pacote (Assistente de Importação e Exportação do SQL Server)
  Depois de especificar e configurar sua fonte e destino de dados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Salvar e executar o pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da configuração, você também poderá salvar as configurações como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacote (SSIS) para personalizá-lo e reutilizá-la posteriormente.
  
**O que é um pacote?** O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. No SSIS, a unidade básica é o pacote. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Captura de tela da página Salvar e Executar Pacote  
A captura de tela a seguir mostra a página **Salvar e Executar o Pacote** do assistente. 
   
![Salve e execute a página do pacote do Assistente de importação e exportação](../../integration-services/import-export-data/media/save-and-run.png "salvar e executar a página do pacote do Assistente de importação e exportação") 
  
## <a name="run-and-save-the-package"></a>Executar e salvar o pacote 
 Para continuar, você precisa selecionar pelo menos uma das duas opções a seguir.  
  
 **Run immediately**  
 Selecione esta opção para importar e exportar dados imediatamente. Por padrão, essa caixa de seleção está selecionada e a operação é executada imediatamente.
  
 **Salvar Pacote SSIS**  
 Salve as configurações como um pacote do SSIS. Opcionalmente, você pode personalizar o pacote e executá-lo novamente posteriormente. Se você optar por salvar o pacote, haverá opções adicionais na próxima página, **Salvar pacote SSIS**.
 
A opção para salvar o pacote estará disponível somente se você tiver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition ou uma edição superior instalada.   
  
> [!NOTE]
> Se você concluir o assistente, execute a operação, mas parar a operação antes que ele termina em execução, o pacote não é salvo, mesmo se você tiver selecionado o **salvar pacote SSIS** caixa de seleção.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Se tiver iniciado o assistente no Visual Studio
Se você iniciou o Assistente de um projeto do Integration Services no Visual Studio com o SQL Server Data Tools (SSDT):
-   Não é possível **executar** o pacote até depois de sair do assistente. Em seguida, você pode executar o pacote do Visual Studio.
-   O assistente **salva** o pacote no projeto do Integration Services do qual você iniciou o assistente.

## <a name="specify-options-for-saving-the-package"></a>Especificar opções para salvar o pacote
**SQL Server**  
 Selecione esta opção para salvar o pacote no SQL Server no **msdb** banco de dados de **sysssispackages** tabela.
 
> [!IMPORTANT]
> Essa opção não salva o pacote no banco de dados do catálogo do SSIS (SSISDB).  

 Selecione o servidor de destino e forneça credenciais para se conectar ao servidor na próxima página, **Salvar pacote SSIS**. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Sistema de arquivos**  
 Selecione esta opção para salvar o pacote como um arquivo com o **dtsx** extensão.  
  
 Selecione a pasta de destino e o nome de arquivo para o pacote na próxima página, **Salvar pacote SSIS**. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Especificar o nível de proteção do pacote
 **Nível de Proteção do Pacote**  
 Selecione um nível de proteção na lista para ajudar a proteger os dados no pacote.  
  
 O nível de proteção determina o método de proteção, a senha ou a chave de usuário, bem como o escopo de proteção do pacote. A proteção pode incluir todos os dados ou apenas os dados confidenciais. Para obter mais informações sobre as opções disponíveis, consulte [Controle de acesso para dados confidenciais em pacotes](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Senha**  
 Digite uma senha.  
  
 **Digite a senha novamente**  
 Digite a senha novamente.  
  
> [!NOTE]
> As opções de senha estão disponíveis apenas se especificar um **nível de proteção do pacote** que requer uma senha - ou seja, se você especificar um **criptografar dados confidenciais com senha** ou **criptografar todos os dados com senha**.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Sobre as duas páginas de opções para salvar o pacote  
 A página **Salvar e executar pacote** é uma das duas páginas nas quais você pode selecionar opções para salvar o pacote do SSIS.  
  
-   Na página atual, escolha se você deseja salvar o pacote no SQL Server ou como um arquivo. Você também pode escolher as configurações de segurança para o pacote salvo.  
  
-   Em seguida, na página **Salvar pacote SSIS** , forneça um nome para o pacote e mais informações sobre onde salvá-lo. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Essas opções estarão disponíveis somente se você selecionar a opção **Salvar pacote SSIS** nesta página.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar se deseja executar a operação de cópia imediatamente e salvar o pacote, a próxima página dependerá das opções que você escolher.  
  
-   Se você tiver escolhido a opção para executar o pacote imediatamente, mas não para salvá-lo, a próxima página será **Concluir o assistente**. Nessa página, examine as escolhas feitas no assistente e inicie a operação de cópia. Para obter mais informações, consulte [Concluir o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Se você tiver selecionado a opção para salvar o pacote, a próxima página será **Salvar pacote SSIS**. Nessa página, você deve especificar as opções adicionais para salvar o pacote. (Depois de salvar o pacote, a página a seguinte será **Concluir o assistente**.) Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Consulte também  
[Salvar pacotes](../../integration-services/save-packages.md)  
[Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Começar com esse exemplo simples de Assistente de importação e exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  


