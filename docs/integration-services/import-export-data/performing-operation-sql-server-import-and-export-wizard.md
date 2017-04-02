---
title: "Executando Opera&#231;&#227;o (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "01/11/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.performingoperation.f1"
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Executando Opera&#231;&#227;o (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
Depois de examinar as escolhas que você fez no assistente e clicar em **Concluir** na página **Concluir o assistente**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Realizando Operação**. Nessa página, você pode ver o andamento e o resultado das operações que você configurou nas páginas anteriores. Você não precisa realizar nenhuma ação nesta página.

## <a name="screen-shot---operation-in-progress"></a>Captura de tela – Operação em andamento 
 A captura de tela a seguir mostra a página **Realizando Operação** do assistente enquanto a operação está em andamento.  
  
 ![Performing operation page of the Import and Export Wizard](../../integration-services/import-export-data/media/performing-operation1.png "Performing operation page of the Import and Export Wizard")  

## <a name="screen-shot---operation-completed"></a>Captura de tela – Operação concluída 
 A captura de tela a seguir mostra a página **Realizando Operação** do assistente depois da conclusão da operação. Clique em um item na coluna **Mensagem** para obter mais informações sobre a etapa correspondente.  
  
 ![Performing operation page of the Import and Export Wizard](../../integration-services/import-export-data/media/performing-operation2.png "Performing operation page of the Import and Export Wizard")  
  
## <a name="watch-the-progress-of-the-operation"></a>Observar o progresso da operação
 **Ação**  
 Exibe cada etapa da operação.  
  
 **Status**  
 Exibe o sucesso ou falha de cada etapa.  
  
 **Mensagem**  
 Exibe mensagens informativas e mensagens de erro sobre a etapa. Clique em um item nesta coluna para obter mais informações sobre a etapa correspondente.

## <a name="interrupt-the-operation-or-save-the-results"></a>Interromper a operação ou salvar os resultados
 **Parar**  
 Interrompa a operação, se necessário, clicando no botão **Parar**.  
  
 **Relatório**  
 Exibe o relatório, salve o relatório em um arquivo, copie-o para a área de transferência ou envie-o por email.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois que a operação que você configurou for executada e concluída com êxito, terminará de executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
-   Se você executar a operação imediatamente, poderá abrir o destino selecionado para analisar os dados copiados pelo assistente.  
-   Se você tiver salvado o pacote do SSIS criado pelo assistente, poderá abri-lo no SQL Server Data Tools para personalizá-lo e reutilizá-lo. Para obter informações sobre como personalizar o pacote salvo e executá-lo novamente mais tarde, consulte [Salvar pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
