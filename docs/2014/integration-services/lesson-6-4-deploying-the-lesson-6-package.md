---
title: 'Etapa 4: implantar o pacote da Lição 6 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
caps.latest.revision: 4
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d62dfcc3587cb2abfe28b2bee899ac38167c4748
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011423"
---
# <a name="step-4-deploying-the-lesson-6-package"></a>Etapa 4: Implantando o pacote da Lição 6
  Implantar o pacote envolve a adição do pacote no catálogo de SSISDB nos Integration Services em uma instância do SQL Server. Nesta lição, você adicionará o pacote da Lição 6 no catálogo SSISDB, definirá o parâmetro e executará o pacote. Nesta lição você usará o SQL Server Management Studio para adicionar o pacote da Lição 6 ao catálogo SSISDB e implantará esse pacote. Depois de implantar o pacote, você modificará o parâmetro para apontar para um novo local e, em seguida, executará o pacote.  
  
 Nesta lição, você irá:  
  
-   Adicionar o pacote ao catálogo de SSISDB no nó SSIS no SQL Server.  
  
-   Implantar o pacote.  
  
-   Definir o valor de parâmetro do pacote.  
  
-   Executar o pacote no SSMS.  
  
### <a name="to-locate-or-add-the-the-ssisdb-catalog"></a>Para localizar ou adicionar ao catálogo do SSISDB  
  
1.  Clique em Iniciar, aponte para Todos os programas, aponte para Microsoft SQL Server 2012 e, em seguida, clique em SQL Management Studio.  
  
2.  Na caixa de diálogo Conectar ao Servidor, verifique as configurações padrão e depois clique em Conectar. Para fazer a conexão, a caixa de diálogo Nome do servidor deve conter o nome do computador em que o SQL Server está instalado. Se o Mecanismo de Banco de Dados for uma instância nomeada, a caixa Nome do Servidor também deverá conter o nome da instância no formato <computer_name>\\<instance_name>.  
  
3.  No Pesquisador de objetos, expanda Catálogos dos Integration Services.  
  
4.  Se não houver nenhum catálogo listado em Catálogos dos Integration Services, adicione o catálogo SSISDB.  
  
5.  Para adicionar o catálogo do SSISDB, clique com botão direito em Catálogos dos Integration Services e clique em Criar catálogo.  
  
6.  Na caixa de diálogo Criar catálogo, selecione Habilitar a integração do CLR.  
  
7.  Digite uma nova senha na caixa Senha; então, digite-a novamente na caixa Confirmar senha. Certifique-se de lembrar a senha que você digitar.  
  
8.  Clique em OK para adicionar o catálogo SSISDB.  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>Para adicionar o pacote ao catálogo SSISDB  
  
1.  No Pesquisador de objetos, clique com o botão direito do mouse em SSISDB e clique em Criar pasta.  
  
2.  Na caixa de diálogo Criar pasta, digite Tutorial do SSIS na caixa de nome de pasta e clique em OK.  
  
3.  Expanda a pasta Tutorial do SSIS, clique com o botão direito do mouse em Projetos e clique em Importar pacotes.  
  
4.  Na página de Introdução do Assistente de conversão de projeto do Integration Services, clique em Avançar.  
  
5.  Na página localizar pacotes, verifique se o sistema de arquivos está selecionado na lista de origem; então, clique em Procurar.  
  
6.  Na caixa de diálogo Procurar pasta, navegue até a pasta que contém o projeto do Tutorial do SSIS e clique em OK.  
  
7.  Clique em Avançar.  
  
8.  Na página Selecionar pacotes, você deve ver todos os seis pacotes do Tutorial do SSIS. Na lista de pacotes, selecione Lição 6.dtsx e clique em Avançar.  
  
9. Na página Selecionar destino, digite Implantação do tutorial do SSIS na caixa Nome do projeto e clique em Avançar.  
  
10. Clique em Avançar em cada uma das páginas restantes do assistente até chegar à página Revisão.  
  
11. Na página Revisão, clique em Converter.  
  
12. Quando a conversão for concluída, clique em Fechar.  
  
 Quando você fecha o Assistente de conversão de projeto do Integration Services, o SSIS exibe o Assistente de implantação do Integration Services. Você agora usará esse assistente para implantar o pacote da Lição 6.  
  
1.  Na página de Introdução do Assistente de implantação do Integration Services, revise as etapas para implantação do projeto e clique em Avançar.  
  
2.  Na página Selecionar destino, verifique se o nome do servidor é a instância do SQL Server que contém o catálogo do SSISDB e o caminho mostra o Implantação do tutorial do SSIS; então, clique em Avançar.  
  
3.  Na página Revisão, revise o resumo e clique em Implantar.  
  
4.  Quando a implantação for concluída, clique em Fechar.  
  
5.  No Pesquisador de objetos, clique com o botão direito do mouse em Catálogos do Integration Services e clique em Atualizar.  
  
6.  Expanda Catálogos do Integration Services e então expanda SSISDB. Continue a expandir a árvore sob Tutorial do SSIS até ter expandido completamente o projeto. Você deve ver Lição 6.dtsx sob o nó Pacotes do nó Implantação do tutorial do SSIS.  
  
 Para verificar se o pacote está concluído, clique com botão direito em Lição 6.dtsx e clique em Configurar. Na caixa de diálogo Configurar, selecione parâmetros e verifique se há uma entrada com a lição 6. dtsx como o contêiner, VarFolderName como o nome e o caminho para a pasta Novos dados de exemplo como o valor; então, clique em Fechar.  
  
 Antes de continuar para criar uma nova pasta de dados de exemplo, nomeie-a Dados de exemplo Dois e copie três arquivos de exemplo originais quaisquer para essa pasta.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>Para criar e popular uma nova pasta de dados de exemplo  
  
1.  No Windows Explorer, no nível da raiz da unidade (por exemplo, C:\\), crie uma nova pasta chamada Dados de Exemplo Dois.  
  
2.  Abra a pasta C:\Program Files\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Criando Um Pacote ETL simples\Dados de Exemplo e, em seguida, copie dos três dos arquivos de exemplo contidos na pasta.  
  
3.  Na pasta Novos Dados de Exemplo, cole os arquivos copiados.  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>Para alterar o parâmetro de pacote para apontar para os novos dados de exemplo  
  
1.  No Pesquisador de objetos, clique com botão direito em Lição 6.dtsx e clique em Configurar.  
  
2.  Na caixa de diálogo Configurar, altere o valor do parâmetro para o caminho da pasta Dados de Exemplo Dois. Por exemplo, C:\Dados de Exemplo Dois se você colocou a nova pasta na raiz da unidade C.  
  
3.  Clique em OK para fechar a caixa de diálogo Configurar.  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>Para testar a implantação de pacote da Lição 6  
  
1.  No Pesquisador de objetos, clique com botão direito em Lição 6.dtsx e clique em Executar.  
  
2.  Na caixa de diálogo Executar pacote, clique em OK.  
  
3.  Na caixa de diálogo de mensagem, clique em Sim para abrir o Relatório de visão geral.  
  
 O Relatório de visão geral do pacote será exibido, mostrando o nome do pacote e um resumo do status. A seção Visão geral de execução mostra o resultado de cada tarefa no pacote, enquanto a seção Parâmetros usados mostra os nomes e valores de todos os parâmetros usados na execução do pacote, incluindo VarFolderName.  
  
  