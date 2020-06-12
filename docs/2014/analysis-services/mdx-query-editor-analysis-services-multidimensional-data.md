---
title: Editor de consultas MDX (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
ms.openlocfilehash: c29ed96b46660808ff54d6997ca438eb0f5a60b8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541708"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>Editor de Consultas MDX (Analysis Services - Dados Multidimensionais)
  Use o Editor de Consultas MDX para criar e executar instruções e scripts escritos na linguagem MDX (Multidimensional Expressions).  
  
## <a name="features"></a>Recursos  
  
-   Digite os scripts no painel do Editor de Consultas MDX.  
  
-   Para executar scripts, pressione **F5**ou clique em **Executar** na barra de ferramentas ou, no menu **Consulta** , clique em **Executar**. Se uma parte do código estiver selecionada, só essa parte será executada. Se nenhum código for selecionado, todo o conteúdo do Editor de Consultas MDX será executado.  
  
-   Exiba metadados para cubos e outros objetos contidos em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no painel de metadados.  
  
-   Para obter ajuda sobre a sintaxe MDX, selecione uma palavra-chave no Editor de Consultas MDX e clique em **F1**.  
  
-   Para obter ajuda dinâmica sobre a sintaxe MDX, no menu **Ajuda** , clique em **Ajuda Dinâmica**para abrir o componente da Ajuda Dinâmica. Com a Ajuda Dinâmica, os tópicos de ajuda aparecem na janela **Ajuda Dinâmica** quando são digitadas palavras-chave no Editor de Consultas.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra de ferramentas de Editores do SQL Server Analysis Services  
 Quando o Editor de Consultas MDX está aberto, a barra de ferramentas dos Editores do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é exibida com os botões listados na tabela a seguir.  
  
|Termo|Definição|  
|----------|----------------|  
|**Connect**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Desligar**|Desconecta o Editor de Consultas MDX de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Alterar Conexão**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância diferente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nova Consulta com Conexão Atual**|Abre uma nova janela Editor de Consultas MDX usando as informações de conexão da janela Editor de Consultas MDX atual.|  
|**Bancos de Dados Disponíveis**|Altera a conexão para outro banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na mesma instância.|  
|**Executados**|Executa o código selecionado ou, se nenhum código estiver selecionado, executa todo o código no Editor de Consultas MDX.|  
|**Passar**|Verifica a sintaxe do código selecionado. Se nenhum código estiver selecionado, esta opção verificará a sintaxe de toda a janela Editor de Consultas MDX.|  
|**Cancelar Consulta de Execução**|Envia uma solicitação de cancelamento ao servidor. Algumas consultas não podem ser canceladas imediatamente, mas precisam esperar por uma condição de cancelamento satisfatória. Quando consultas são canceladas, podem ocorrer atrasos enquanto as transações são convertidas.|  
  
## <a name="mdx-query-editor-window"></a>Janela Editor de Consultas MDX  
 As opções listadas na tabela a seguir estão disponíveis no Editor de Consultas MDX.  
  
|Termo|Definição|  
|----------|----------------|  
|**janela Editor de consultas**|Digite as instruções e scripts MDX a serem executadas pelo Editor de Consultas MDX.<br /><br /> O menu de contexto do editor de consultas fornece as seguintes opções:<br /><br /> **Recortar**: copia a seleção atual para a área de transferência e remove a seleção da janela do editor de consultas.<br /><br /> **Copiar**: copia a seleção atual para a área de transferência.<br /><br /> **Colar**: cola o conteúdo da área de transferência na seleção atual.<br /><br /> **Conectar**: abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Desconectar: desconecta**o editor de consultas atual de uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância.<br /><br /> **Desconectar todas as consultas: desconecta**todos os editores de consulta abertos no momento.<br /><br /> **Alterar conexão**: abre a caixa de diálogo **conectar ao servidor** para estabelecer uma conexão com uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância diferente.<br /><br /> **Abrir servidor no Pesquisador de objetos**: abre a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância para a qual o editor de consultas atual está conectado no **pesquisador de objetos**.<br /><br /> **Execute**: execute o código selecionado ou, se nenhum código estiver selecionado, executará o código inteiro no editor de consultas atual.<br /><br /> **Janela Propriedades**: exibe a janela **Propriedades** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para a janela de consulta atual.<br /><br /> **Opções de consulta**: exibe a caixa de diálogo **Opções de consulta** .|  
|**Janela Metadados**|Exibe metadados para o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] conectado no momento.|  
|**Simples**|Selecione um cubo no banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] conectado no momento para exibir os metadados associados ao cubo na guia **Metadados** .|  
|**Metadados**|Exibe os metadados do cubo selecionado em **Cubo**, incluindo grupos de medidas e medidas, indicadores chave de desempenho, dimensões, hierarquias, níveis, membros e propriedades de membros. Para recuperar a chave completamente qualificada de um objeto, proceda de uma das seguintes maneiras:<br /><br /> Arraste o objeto da guia **Metadados** para o painel de consulta.<br /><br /> Clique com o botão direito do mouse no objeto e selecione **Copiar**e clique com o botão direito do mouse no painel de consulta e selecione **Colar**.|  
|**Funções**|Exibe os metadados de funções MDX disponíveis para o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , conforme recuperados do conjunto de linhas do esquema MDSCHEMA_FUNCTIONS. Para recuperar a sintaxe de uma função, proceda de uma das seguintes maneiras:<br /><br /> Arraste o objeto da guia **Funções** para o painel de consulta.<br /><br /> Clique com o botão direito do mouse na função e selecione **Copiar**e clique com o botão direito do mouse no painel de consulta e selecione **Colar**.|  
|**Janela Resultados**|Exibe os resultados de uma instrução ou script MDX em uma grade.|  
|**Janela Mensagens**|Exibe informações sobre como uma instrução ou um script MDX foi executado. Por exemplo, esta janela exibe todos os erros encontrados durante a execução ou o número de células recuperados depois da execução.|  
  
  
