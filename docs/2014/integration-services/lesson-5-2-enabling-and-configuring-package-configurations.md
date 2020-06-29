---
title: 'Etapa 2: configurar e habilitar configurações de pacote | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: da51560f2ccfb7bef849f1b191c43f19d35d36ed
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440383"
---
# <a name="step-2-enabling-and-configuring-package-configurations"></a>Etapa 2: Habilitar e configurar configurações de pacote
  Nesta tarefa, você converterá o projeto no Modelo de Implantação de Pacote e habilitará configurações de pacote usando o Assistente de Configuração de Pacotes. Você usará esse assistente para gerar um arquivo de configuração XML que contenha definições de configuração para a propriedade `Directory` do contêiner Loop Foreach. O valor da propriedade de diretório é fornecido por uma nova variável de nível de pacote que você pode atualizar no tempo de execução. Adicionalmente, você populará uma pasta de dados de exemplo para usar durante o teste.  
  
### <a name="to-create-a-new-package-level-variable-mapped-to-the-directory-property"></a>Para criar uma nova variável de nível de pacote mapeada para a propriedade de diretório  
  
1.  Clique na tela de fundo da guia **Fluxo de Controle** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Isso define o escopo da variável que você criará para o pacote.  
  
2.  No menu [!INCLUDE[ssIS](../includes/ssis-md.md)] , selecione **Variáveis**.  
  
3.  Na janela **Variáveis** , clique no ícone Adicionar Variável.  
  
4.  Na caixa **Nome** , digite **varFolderName**.  
  
    > [!IMPORTANT]  
    >  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
5.  Verifique se a caixa **escopo** mostra o nome do pacote, lição 5.  
  
6.  Defina o valor da caixa **Tipo de Dados** da variável `varFolderName` como **Cadeia de Caracteres**.  
  
7.  Retorne à guia **Fluxo de Controle** e clique duas vezes no contêiner **Arquivo Foreach na Pasta** .  
  
8.  Na página **coleção** do editor de **loop foreach**, clique em **expressões**e, em seguida, clique no botão de reticências **(...)**.  
  
9. No **Editor de expressões de propriedade**, clique na lista de **Propriedades** e selecione `Directory` .  
  
10. Na caixa **expressão** , clique no botão de reticências **(...)**.  
  
11. No **Construtor de Expressões**, expanda a pasta Variáveis e arraste a variável **User::varFolderName** até a caixa **Expressão** .  
  
12. Clique em **OK** para sair do **Construtor de Expressões**.  
  
13. Clique em **OK** para sair do **Editor de Expressões de Propriedades**.  
  
14. Clique em **OK** para sair do **Editor do Loop Foreach**.  
  
### <a name="to-enable-package-configurations"></a>Para habilitar configurações de pacote  
  
1.  No **menu Projeto**, clique em **converter em modelo de implantação de pacote**.  
  
2.  Clique em **OK** no aviso e, assim que a conversão for concluída, clique em **OK** na caixa de diálogo **Converter em Modelo de Implantação de Pacote** .  
  
3.  Clique na tela de fundo da guia **Fluxo de Controle** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
4.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
5.  Na caixa de diálogo **Organizador de Configurações do Pacote** , selecione **Habilitar Configurações do Pacote**e clique em **Adicionar**.  
  
6.  Na página inicial do assistente de configuração de pacotes, clique em **Avançar**.  
  
7.  Na página **Selecionar Tipo de Configuração** , verifique se o **Tipo de configuração** está definido como **Arquivo de configuração XML**.  
  
8.  Na página **Selecionar Tipo de Configuração** , clique em **Procurar**.  
  
9. Por padrão, a caixa de diálogo **Selecionar Local do Arquivo de Configuração** abrirá a pasta do projeto.  
  
10. Na caixa de diálogo **Selecionar Local do Arquivo de Configuração** , em **Nome do arquivo** , digite **SSISTutorial**e clique em **Salvar**.  
  
11. Na página **Selecionar Tipo de Configuração** , clique em **Avançar**.  
  
12. Na página **selecionar propriedades a serem exportadas** , no painel **objetos** , expanda **variáveis**, expanda **varFolderName**, **Propriedades**e selecione **valor**.  
  
13. Na página **Selecionar Propriedades para Exportar** , clique em **Avançar**.  
  
14. Na página **Concluindo o Assistente** , digite um nome de configuração para a configuração, como **Configuração do Diretório de Tutoriais do SSIS**. Esse é o nome de configuração exibido na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
15. Clique em **Concluir**.  
  
16. Clique em **fechar**  
  
17. O assistente cria um arquivo de configuração, chamado SSISTutorial.dtsConfig, que contém as definições de configuração de `value` da variável que define a propriedade `Directory` do enumerador.  
  
    > [!NOTE]  
    >  Um arquivo de configuração geralmente contém informações complexas sobre as propriedades do pacote, mas, para este tutorial, a única informação de configuração deveria ser  
    > <Configuration ConfiguredType="Property"  
    > Path = "\Package.Variables [User:: varFolderName]. Properties [valor] "ValueType =" cadeia de caracteres "\>  
    >  \<ConfiguredValue>\</ConfiguredValue>  
    > \</Configuration>.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>Para criar e popular uma nova pasta de dados de exemplo  
  
1.  No Windows Explorer, no nível raiz da unidade (por exemplo, C: \\ ), crie uma nova pasta chamada `New Sample Data` .  
  
2.  Localize os arquivos de exemplo no computador e copie três dos arquivos da pasta.  
  
3.  Na `New Sample Data` pasta, Cole os arquivos copiados.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 3: Modificar o valor de configuração da propriedade de diretório](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
  
