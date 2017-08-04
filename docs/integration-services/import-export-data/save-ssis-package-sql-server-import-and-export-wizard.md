---
title: "Salvar pacote SSIS (SQL Server Assistente de importação e exportação) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 6ebbab742350e6874b86213c1fbf516e095a1e9a
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Salvar Pacote SSIS (Assistente de Importação e Exportação do SQL Server)
  Se você especificou no **salvar e executar pacote** página que você deseja salvar as configurações como um pacote do SQL Server Integration Services (SSIS), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra Import and Export Wizard **salvar pacote SSIS**. Nessa página, você deve especificar opções adicionais para salvar o pacote criado pelo assistente.  

As opções que você vê na página **Salvar Pacote SSIS** dependem da opção que você fez anteriormente na página **Salvar e Executar Pacote** para salvar o pacote no SQL Server ou no sistema de arquivos. Para ver novamente a página **Salvar e Executar Pacote** , consulte [Salvar e Executar Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**O que é um pacote?** O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. No SSIS, a unidade básica é o pacote. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.

## <a name="screen-shot---common-options"></a>Captura de tela de - opções comuns
A captura de tela a seguir mostra a primeira parte do **salvar pacote SSIS** página do assistente. O restante da página tem um número variável de opções que dependem do destino do pacote que você escolheu.

![Salvar pacote - opções comuns](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>Forneça um nome e uma descrição para o pacote  
 **Nome**  
 Forneça um nome exclusivo para o pacote.  
  
 **Descrição**  
 Forneça uma descrição para o pacote. Como prática recomendada, descreva o pacote em termos de objetivo, para facilitar a documentação e a manutenção dos pacotes.  
  
 **Target (destino)**  
 O destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Sistema de arquivos) especificado anteriormente para o pacote. Se desejar salvar o pacote em um destino diferente, volte para a página **Salvar e Executar Pacote** .

## <a name="screen-shot---save-the-package-in-sql-server"></a>Captura de tela – Salvar o pacote no SQL Server

 Captura de tela a seguir mostra o **salvar pacote SSIS** página do assistente, se você tiver selecionado o **do SQL Server** opção o **salvar e executar pacote** página. 
  
![Salvar pacote SSIS página do Assistente de importação e exportação](../../integration-services/import-export-data/media/save-package2.png "página Salvar pacote SSIS do Assistente de importação e exportação")  

## <a name="options-to-specify-target--sql-server"></a>Opções para especificar (destino = SQL Server) 

 > [!NOTE]
 > O assistente salva o pacote no **msdb** banco de dados de **sysssispackages** tabela. Esta opção faz **não** salvar o pacote para o banco de dados do catálogo do SSIS (SSISDB).  
 
 **Nome do servidor**  
 Digite ou selecione o nome do servidor de destino.  
   
 **Usar Autenticação do Windows**  
Conecte-se ao servidor usando a Autenticação Integrada do Windows. Esse é o método de autenticação preferido.  
  
 **Usar Autenticação do SQL Server**  
Conecte-se ao servidor usando a Autenticação do SQL Server.  
  
 **Nome de usuário**  
Se você especificou a autenticação do SQL Server, digite o nome de usuário.  
  
 **Senha**  
Se você especificou a autenticação do SQL Server, digite a senha.  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Captura de tela – Salvar o pacote no sistema de arquivos
 
Captura de tela a seguir mostra o **salvar pacote SSIS** página do assistente, se você tiver selecionado o **sistema de arquivos** opção o **salvar e executar pacote** página. 
  
![Salvar pacote SSIS página do Assistente de importação e exportação](../../integration-services/import-export-data/media/save-package1.png "página Salvar pacote SSIS do Assistente de importação e exportação")  

## <a name="options-to-specify-target--file-system"></a>Opções para especificar (destino = sistema de arquivos)

 **Nome do arquivo**  
 Digite o caminho e o nome de arquivo para o arquivo de destino ou use o **procurar** para selecionar um destino.  
  
> [!TIP]
> Certifique-se de especificar uma pasta de destino, inserindo-a ou navegando. Se você inserir apenas o nome do arquivo sem um caminho, você não sabe onde o assistente salva o pacote. Além disso, o assistente pode tentar salvar o pacote em um local no qual você não tem permissão para salvar um arquivo e gerar um erro.  
>   
>  Lembre-se de onde você salvou o arquivo de pacote.  
  
 **Procurar**  
 Como opção, navegue para selecionar o caminho do arquivo de destino no **salvar pacote** caixa de diálogo.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Sobre as duas páginas de opções para salvar o pacote  
 A página **Salvar Pacote do SSIS** é uma das duas páginas nas quais você pode selecionar opções para salvar o pacote do SSIS.  
  
-   Na página anterior, **Salvar e Executar Pacote**, escolha se você deseja salvar o pacote no SQL Server ou como um arquivo. Você também pode escolher as configurações de segurança para o pacote salvo. Para ver novamente a página **Salvar e Executar Pacote** , consulte [Salvar e Executar Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
  
-   Na página atual, forneça um nome para o pacote e mais informações sobre onde salvá-lo.  
 
## <a name="run-the-saved-package-again-later"></a>Executar o pacote salvo mais tarde  
 Para saber como executar o pacote salvo mais tarde, consulte um dos tópicos a seguir.  
  
-   Para executar um pacote usando um programa utilitário com uma interface de usuário amigável, consulte [Referência de Interface do Usuário do Utilitário de Execução de Pacotes &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).  
  
-   Para executar um pacote de uma linha de comando ou de um arquivo em lotes, consulte [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md).  
  
-   Se tiver salvado o pacote no SQL Server no banco de dados **msdb** , conecte-se ao serviço do Integration Services. Em seguida, no SQL Server Management Studio, no Pesquisador de Objetos, navegue até **Pacotes Armazenados | MSDB**, clique com o botão direito do mouse no pacote e selecione **Executar Pacote**.

-   Se tiver salvado o pacote no sistema de arquivos, consulte [Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md) para executar o pacote no ambiente de desenvolvimento. Você precisa adicionar o pacote a um projeto do Integration Services antes de poder abrir e executá-lo.  

## <a name="customize-the-saved-package"></a>Personalizar o pacote salvo  
 Para saber como personalizar o pacote salvo, consulte [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md).  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar opções adicionais para salvar o pacote, a página seguinte é **Concluir o assistente**. Nessa página, examine as escolhas feitas no assistente e inicie a operação. Para obter mais informações, consulte [Concluir o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>Consulte também  
[Salvar pacotes](../../integration-services/save-packages.md)  
[Executar pacotes do SSIS (Integration Services)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 

