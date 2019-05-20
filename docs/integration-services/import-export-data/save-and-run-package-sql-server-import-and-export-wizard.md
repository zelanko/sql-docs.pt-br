---
title: Salvar e executar Pacote (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8326920e557d6ed304414f96a7da040de0093dd0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723734"
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Salvar e Executar Pacote (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Depois de especificar e configurar sua fonte e destino de dados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Salvar e executar o pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da sua configuração, você também poderá salvar suas configurações como um pacote SSIS ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) para personalizá-lo e reutilizá-lo posteriormente.
  
**O que é um pacote?** O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. No SSIS, a unidade básica é o pacote. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Captura de tela da página Salvar e Executar Pacote  
A captura de tela a seguir mostra a página **Salvar e Executar o Pacote** do assistente. 
   
![Página Salvar e executar pacote do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/save-and-run.png "Página Salvar e executar pacote do Assistente de Importação e Exportação") 
  
## <a name="run-and-save-the-package"></a>Executar e salvar o pacote 
 Para continuar, você precisa selecionar pelo menos uma das duas opções a seguir.  
  
 **Run immediately**  
 Selecione esta opção para importar e exportar dados imediatamente. Por padrão, essa caixa de seleção é marcada e a operação é executada imediatamente.
  
 **Salvar Pacote SSIS**  
 Salve as configurações como um pacote SSIS. Opcionalmente, você pode personalizar o pacote e executá-lo novamente posteriormente. Se você optar por salvar o pacote, haverá opções adicionais na próxima página, **Salvar pacote SSIS**.
 
A opção para salvar o pacote estará disponível somente se você tiver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition ou uma edição superior instalada.   
  
> [!NOTE]
> Se você concluir o assistente, executar a operação mas interrompê-la antes da execução dela terminar, o pacote não será salvo mesmo que a caixa de seleção **Salvar Pacote SSIS** tenha sido marcada nesta página.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Se você iniciou o assistente do Visual Studio
Se você iniciou o assistente de um projeto do Integration Services no Visual Studio com o SSDT (SQL Server Data Tools):
-   Não é possível **executar** o pacote antes de sair do assistente. Em seguida, você poderá executar o pacote do Visual Studio.
-   O assistente **salva** o pacote no projeto do Integration Services do qual você iniciou o assistente.

## <a name="specify-options-for-saving-the-package"></a>Especificar opções para salvar o pacote
**SQL Server**  
 Selecione esta opção para salvar o pacote SQL Server no banco de dados **msdb** na tabela **sysssispackages**.
 
> [!IMPORTANT]
> Essa opção não salva o pacote no banco de dados do catálogo do SSIS (SSISDB).  

 Selecione o servidor de destino e forneça credenciais para se conectar ao servidor na próxima página, **Salvar pacote SSIS**. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Sistema de arquivos**  
 Selecione essa opção para salvar o pacote como um arquivo com extensão **.dtsx**.  
  
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
> As opções de senha só estarão disponíveis se você especificar um **Nível de proteção do pacote** que requer uma senha – ou seja, se você especificar **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas**.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Sobre as duas páginas de opções para salvar o pacote  
 A página **Salvar e executar pacote** é uma das duas páginas nas quais você pode selecionar opções para salvar o pacote do SSIS.  
  
-   Na página atual, escolha se você deseja salvar o pacote no SQL Server ou como um arquivo. Você também pode escolher as configurações de segurança para o pacote salvo.  
  
-   Em seguida, na página **Salvar pacote SSIS** , forneça um nome para o pacote e mais informações sobre onde salvá-lo. Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Essas opções estarão disponíveis somente se você selecionar a opção **Salvar pacote SSIS** nesta página.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar se deseja executar a operação de cópia imediatamente e salvar o pacote, a próxima página dependerá das opções que você escolher.  
  
-   Se você tiver escolhido a opção para executar o pacote imediatamente, mas não para salvá-lo, a próxima página será **Concluir o assistente**. Nessa página, examine as escolhas feitas no assistente e inicie a operação de cópia. Para obter mais informações, consulte [Concluir o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Se você tiver selecionado a opção para salvar o pacote, a próxima página será **Salvar pacote SSIS**. Nessa página, você deve especificar as opções adicionais para salvar o pacote. (Depois de salvar o pacote, a página a seguinte será **Concluir o assistente**.) Para obter mais informações, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Consulte Também  
[Salvar pacotes](../../integration-services/save-packages.md)  
[Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

