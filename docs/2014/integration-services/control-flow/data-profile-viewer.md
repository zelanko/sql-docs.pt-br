---
title: Visualizador de Perfil de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0f6bcad3636178fb4aebbcdbeee29ba2542f092e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62832355"
---
# <a name="data-profile-viewer"></a>Visualizador de Perfil de Dados
  Exibir e analisar os perfis de dados são a próxima etapa no processo de criação de perfil de dados. Esses perfis podem ser exibidos depois que você executar a tarefa Criação de Perfil de Dados dentro de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e computá-los. Para obter mais informações sobre como configurar e executar a tarefa Criação de Perfil de Dados, consulte [Configuração da Tarefa Criação de Perfil de Dados](data-profiling-task.md).  
  
> [!IMPORTANT]  
>  O arquivo de saída pode conter dados confidenciais sobre seu banco de dados e os dados contidos no banco de dados. Para obter sugestões sobre como tornar esse arquivo mais seguro, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
## <a name="data-profiles"></a>Perfis de dados  
 Para exibir os perfis, configure a tarefa Criação de Perfil de Dados para enviar a saída a um arquivo e use o Visualizador de Perfil de Dados de maneira autônoma. Para abrir o Visualizador de Perfil de Dados, execute um dos procedimentos a seguir.  
  
-   Clique com o botão direito do mouse na tarefa **Criação de Perfil de Dados** no Designer de [!INCLUDE[ssIS](../../includes/ssis-md.md)] e clique em **Editar**. Clique em **Abrir o Visualizador de Perfil** na página **Geral** de **Editor da Tarefa Criação de Perfil de Dados**.  
  
-   Na pasta *\<unidade>* :\Arquivos de Programas (x86) | Arquivos de Programas\Microsoft SQL Server\110\DTS\Binn, execute o DataProfileViewer.exe.  
  
 O visualizador usa vários painéis para exibir os perfis solicitados e os resultados computados, com detalhes e capacidade de busca opcionais:  
  
 Painel**Perfis**  
 O painel **Perfis** exibe os perfis que foram solicitados na tarefa Perfil de Dados. Para exibir os resultados computados do perfil, selecione o perfil no painel **Perfis** e os resultados serão exibidos nos outros painéis do visualizador.  
  
 Painel**Resultados**  
 O painel **Resultados** usa apenas uma linha para resumir os resultados computados do perfil. Por exemplo, ao solicitar um **Perfil de Distribuição de Comprimento de Coluna**, essa linha incluirá os dados de comprimento máximo e mínimo, além da contagem da linha. Em muitos perfis, é possível selecionar essa linha no painel **Resultados** para ver detalhes adicionais no painel **Detalhes** (opcional).  
  
 Painel**Detalhes**  
 Para muitos tipos de perfil, o painel **Detalhes** exibe informações adicionais sobre os resultados de perfil selecionados no painel **Resultados** . Por exemplo, se você solicitar um **Perfil de Distribuição de Comprimento de Coluna**, o painel **Detalhes** exibirá todos os comprimentos de coluna encontrados. O painel também exibe o número e a porcentagem de linhas nas quais o valor de coluna tem esse comprimento de coluna.  
  
 Para os três tipos de perfil que são computados em mais de uma coluna (Perfil Chave de Candidato, Dependência Funcional e Inclusão de Valor), o painel **Detalhes** exibe as violações da relação esperada. Por exemplo, se você solicitar um Perfil Chave de Candidato, o painel Detalhes exibirá valores duplicados que violam a exclusividade da chave candidata.  
  
 Se a fonte de dados usada para computar o perfil estiver disponível, você poderá clicar duas vezes em uma linha no painel **Detalhes** para ver as linhas de dados correspondentes no painel **Busca Detalhada** .  
  
 Painel**Busca Detalhada**  
 Clique duas vezes em uma linha no painel **Detalhes** para ver as linhas de dados correspondentes no painel **Busca Detalhada** quando as seguintes condições forem verdadeiras:  
  
-   A fonte de dados usada para computar o perfil está disponível.  
  
-   Você tem permissão para exibir os dados.  
  
 Para conectar ao banco de dados de origem para uma solicitação de busca detalhada, o Visualizador de Perfil de Dados usa a Autenticação do Windows e as credenciais do usuário atual. O Visualizador de Perfil de Dados não usa as informações de conexão armazenadas no pacote que executou a tarefa Criação de Perfil de Dados.  
  
> [!IMPORTANT]  
>  O recurso de busca detalhada que está disponível no Visualizador de Perfil de Dados envia consultas ao vivo à fonte de dados original. Essas consultas podem ter um impacto negativo no desempenho do servidor.  
>   
>  Se você fizer uma busca detalhada em um arquivo de saída que não foi criado recentemente, as consultas de busca detalhada poderão retornar um conjunto diferente de linhas daquelas nas quais a saída original foi calculada.  
  
 Para obter mais informações sobre a interface do usuário do Visualizador de Perfil de Dados, consulte [Ajuda de F1 do Visualizador de Perfil de Dados](../data-profile-viewer-f1-help.md).  
  
  
