---
description: 'Lição 5-2: Habilitar e configurar as configurações do pacote'
title: 'Etapa 2: Habilitar e configurar as configurações do pacote | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7237d7356ffb97861779c4d5427fd4fb05083695
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88345322"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>Lição 5-2: Habilitar e configurar as configurações do pacote

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Nesta tarefa, você converterá o projeto no Modelo de Implantação de Pacote e habilitará configurações de pacote usando o Assistente de Configuração de Pacotes. Você usará esse assistente para gerar um arquivo de configuração XML que contém definições de configuração da propriedade **Directory** do contêiner Loop Foreach. O valor da propriedade **Directory** é fornecido por uma nova variável de nível de pacote que você pode atualizar no tempo de execução. Você também pode preencher uma nova pasta de dados de exemplo para uso em testes.  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>Crie uma variável em nível de pacote mapeada para a propriedade Directory  
  
1.  Selecione a tela de fundo da guia **Fluxo de Controle** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)]. Essa seleção define o escopo da variável que você criará para o pacote.  
  
2.  No menu [!INCLUDE[ssIS](../includes/ssis-md.md)] , selecione **Variáveis**.  
  
3.  Na janela **Variáveis**, selecione o ícone **Adicionar Variável**.  
  
4.  Na caixa **Nome**, insira **varFolderName**.  
  
    > [!IMPORTANT]  
    > Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
5.  Verifique se a caixa **Escopo** mostra o nome do pacote, **Lição 5**.  
  
6.  Defina o valor da caixa **Tipo de Dados** da variável `varFolderName` como **Cadeia de Caracteres**.  
  
7.  Retorne à guia **Fluxo de Controle** e clique duas vezes no contêiner **Arquivo Foreach na Pasta** .  
  
8.  Na página **Coleção** do **Editor de Loop Foreach**, selecione **Expressões** e, em seguida, selecione o botão de reticências **(…)**.  
  
9. No **Editor de Expressões de Propriedades**, selecione a lista **Propriedade** e selecione **Directory**.  
  
10. Na caixa **Expressão**, selecione o botão de reticências **(…)**.  
  
11. No **Construtor de Expressões**, expanda a pasta **Variáveis e Parâmetros** e arraste a variável **User::varFolderName** até a caixa **Expressão**.  
  
12. Selecione **OK** para sair do **Construtor de Expressões**.  
  
13. Selecione **OK** para sair do **Editor de Expressões de Propriedades**.  
  
14. Selecione **OK** para sair do **Editor do Loop Foreach**.  
  
## <a name="enable-package-configurations"></a>Habilitar configurações de pacote  
  
1.  No **Menu do Projeto**, selecione **Converter em Modelo de Implantação de Pacote**.  
  
2.  Selecione **OK** no aviso e, assim que a conversão for concluída, selecione **OK** na caixa de diálogo **Converter em Modelo de Implantação de Pacote**.  
  
3.  Selecione a tela de fundo da guia **Fluxo de Controle** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
4.  No menu **SSIS**, selecione **Configurações do Pacote**.  
  
5.  Na caixa de diálogo **Organizador de Configurações do Pacote**, selecione **Habilitar Configurações do Pacote** e selecione **Adicionar**.  
  
6.  Na página inicial do **Assistente de Configuração de Pacotes**, selecione **Avançar**.  
  
7.  Na página **Selecionar Tipo de Configuração** , verifique se o **Tipo de configuração** está definido como **Arquivo de configuração XML**.  
  
8.  Na página **Selecionar Tipo de Configuração**, selecione **Procurar**.  
  
9. A caixa de diálogo **Selecionar Local do Arquivo de Configuração** é aberta para a pasta do projeto.  
  
10. Na caixa de diálogo **Selecionar Local do Arquivo de Configuração**, para **Nome do arquivo**, insira **SSISTutorial** e selecione **Salvar**.  
  
11. Na página **Selecionar Tipo de Configuração**, selecione **Avançar**.
  
12. Na página **Selecionar Propriedades para Exportar**, no painel **Objetos**, expanda **Variáveis**, **varFolderName**, **Propriedades** e selecione **Valor**.  
  
13. Na página **Selecionar Propriedades para Exportar**, selecione **Avançar**.  
  
14. Na página **Concluindo o Assistente**, insira um nome de configuração para a configuração, como **Configuração do Diretório de Tutoriais do SSIS**. O nome de configuração é exibido na caixa de diálogo **Organizador de Configurações do Pacote**.  
  
15. Selecione **Concluir**.  
  
16. Selecione **Fechar**.  
  
17. O assistente cria um arquivo de configuração, chamado **SSISTutorial.dtsConfig**, que contém as definições de configuração do **Valor** da variável que, por sua vez, define a propriedade **Directory** do enumerador.  
  
    > [!NOTE]  
    > Um arquivo de configuração geralmente contém informações complexas sobre as propriedades do pacote, mas, para este tutorial, a única informação de configuração deveria ser a seguinte:

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Criar e popular uma nova pasta de dados de exemplo  
  
1.  No Windows Explorer, no nível de raiz da unidade (por exemplo, **C:\\**), crie uma pasta chamada **Novos Dados de Exemplo**.  
  
2.  Localize os arquivos de exemplo no computador e copie três dos arquivos da pasta.  
  
3.  Na pasta **Novos Dados de Exemplo** , cole os arquivos copiados.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 3: Modificar o valor de configuração da propriedade Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
