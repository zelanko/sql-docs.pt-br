---
title: Editor de consultas DMX (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3be28b0a402743e4d9c26b346386202127c5f74d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081575"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>Editor de Consultas DMX (Analysis Services – Mineração de Dados)
  Utilize o Editor de Consultas DMX para criar e executar instruções gravadas na linguagem DMX.  
  
## <a name="features"></a>Recursos  
  
-   Digite os scripts no painel do editor de consultas do Editor de Consultas DMX.  
  
-   Para executar scripts, pressione **F5**ou clique em **Executar** na barra de ferramentas ou no menu **Consulta** . Se uma parte do código estiver selecionada, só essa parte será executada. Se nenhum código for selecionado, todo o conteúdo do Editor de Consultas DMX será executado.  
  
-   Visualizar metadados de cubos e outros objetos contidos em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no painel de metadados.  
  
-   Para obter ajuda sobre a sintaxe DMX, selecione uma palavra-chave no Editor de Consultas DMX e clique em **F1**.  
  
-   Para obter ajuda dinâmica sobre a sintaxe DMX, no menu **Ajuda** , clique em **Ajuda Dinâmica** para abrir o componente Ajuda Dinâmica. Com a Ajuda Dinâmica, os tópicos de ajuda aparecem na janela **Ajuda Dinâmica** quando são digitadas palavras-chave no Editor de Consultas.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra de ferramentas de Editores do SQL Server Analysis Services  
 Quando o Editor de Consultas DMX está aberto, a barra de ferramentas dos **Editores do SQL Server Analysis Services** aparece com os botões listados na tabela a seguir.  
  
|Termo|Definição|  
|----------|----------------|  
|**Connect**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância do Analysis Services.|  
|**Desconectar**|Desconecta o Editor de Consultas DMX de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Alterar Conexão**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância diferente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nova Consulta com Conexão Atual**|Abre uma nova janela do Editor de Consultas DMX, utilizando as informações de conexão da janela atual do Editor de Consultas DMX.|  
|**Bancos de Dados Disponíveis**|Altera a conexão para outro banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na mesma instância.|  
|**Executar**|Executa o código selecionado ou, se nenhum código for selecionado, esta opção executará todo o código no Editor de Consultas DMX.|  
|**Analisar**|Verifica a sintaxe do código selecionado. Se nenhum código for selecionado, essa opção verificará a sintaxe de toda a janela Editor de Consultas DMX.|  
|**Cancelar Consulta de Execução**|Envia uma solicitação de cancelamento ao servidor. Algumas consultas não podem ser canceladas imediatamente, mas precisam esperar por uma condição de cancelamento satisfatória. Quando canceladas, podem ocorrer atrasos enquanto as transações são revertidas.|  
  
## <a name="dmx-query-editor-window"></a>Janela Editor de Consultas DMX  
 As opções listadas na tabela a seguir estão disponíveis no Editor de Consultas MDX.  
  
|Termo|Definição|  
|----------|----------------|  
|**Janela editor de consultas**|Digite as instruções e os scripts DMX a serem executados pelo Editor de Consultas DMX.<br /><br /> O menu de contexto do editor de consultas fornece as seguintes opções:<br /><br /> **Recortar**: Copia a seleção atual na área de transferência e remove a seleção da janela do editor de consultas.<br /><br /> **Copiar**: Copia a seleção atual na área de transferência.<br /><br /> **Colar**: Cola o conteúdo da área de transferência na seleção atual.<br /><br /> **Conectar**: Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Desconectar**: Desconecta o editor de consultas atual de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Desconectar Todas as Consultas**: Desconecta todos os editores de consulta abertos.<br /><br /> **Alterar Conexão**: Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância diferente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Abrir Servidor no Pesquisador de Objetos**: Abre a caixa de diálogo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] com a qual o editor de consultas atual está conectado no **Pesquisador de Objetos**.<br /><br /> **Executar**: Executa o código selecionado ou, se nenhum código estiver selecionado, executa todo o código no editor de consultas atual.<br /><br /> **Janela Propriedades**: Exibe a janela **Propriedades** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da janela de consultas atual.<br /><br /> **Opções de Consulta**: Exibe a caixa de diálogo **Opções de Consulta** .|  
|**Janela metadados**|Exibe metadados para o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] conectado no momento.|  
|**Cube**|Selecione um cubo no banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] conectado no momento para exibir os metadados associados ao cubo na guia **Metadados** .|  
|**Metadados**|Exibe os metadados do cubo selecionado em **Cubo**, incluindo grupos de medidas e medidas, indicadores chave de desempenho, dimensões, hierarquias, níveis, membros e propriedades de membros. Para recuperar a chave completamente qualificada de um objeto, proceda de uma das seguintes maneiras:<br /><br /> Arraste o objeto da guia **Metadados** para o painel de consulta.<br /><br /> Ou:<br /><br /> Clicar com o botão direito do mouse sobre o objeto e selecionar **Copiar**e, depois, clicar com o botão direito do mouse no painel de consultas e selecionar **Colar**.|  
|**Funções**|Exibe os metadados de funções DMX disponíveis para o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , conforme recuperados do conjunto de linhas de esquema DMSCHEMA_MINING_FUNCTIONS.<br /><br /> Para recuperar a sintaxe de uma função, proceda de uma das seguintes maneiras:<br /><br /> Arraste o objeto da guia **Funções** para o painel de consulta.<br /><br /> Ou:<br /><br /> Clique com o botão direito do mouse na função e selecione **Copiar**e clique com o botão direito do mouse no painel de consulta e selecione **Colar**.|  
|**Janela de resultados**|Exibe os resultados de uma instrução DMX em uma grade.|  
|**Janela mensagens**|Exibe informações sobre como uma instrução DMX foi executada. Por exemplo, esta janela exibe todos os erros encontrados durante a execução ou o número de células recuperados depois da execução.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Referência de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Editor de consultas MDX &#40;Analysis Services - dados multidimensionais&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Editor de consultas XMLA &#40;Analysis Services - dados multidimensionais&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [Consulta e editores de texto &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Atalhos de teclado do SQL Server Management Studio](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [Personalizar Menus e teclas de atalho](../ssms/customize-menus-and-shortcut-keys.md)   
 [Codificação por cores nos Editores de Consulta](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
