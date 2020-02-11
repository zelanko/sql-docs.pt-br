---
title: Editor de Consultas XMLA (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.editor.xmla.f1
helpviewer_keywords:
- XMLA Query Editor
- Query Editor [XMLA]
ms.assetid: 14623019-7839-4038-9d12-2f8953d2ec04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1939ea9e1de7b0b7858ad09ad26bc3b4fbf008c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065309"
---
# <a name="xmla-query-editor-analysis-services---multidimensional-data"></a>Editor de Consultas XMLA (Analysis Services – Dados Multidimensionais)
  Use o Editor de Consultas XMLA para criar e executar instruções e scripts escritos na linguagem XMLA (Multidimensional Expressions).  
  
## <a name="features"></a>Recursos  
  
-   Digite os scripts no painel do Editor de Consultas XMLA.  
  
-   Para executar scripts, pressione **F5**ou clique em **Executar** na barra de ferramentas ou, no menu **Consulta** , clique em **Executar**. Se uma parte do código estiver selecionada, só essa parte será executada. Se nenhum código for selecionado, todo o conteúdo do Editor de Consultas XMLA será executado.  
  
-   Exiba metadados para cubos e outros objetos contidos em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no painel de metadados.  
  
-   Para obter ajuda sobre a sintaxe XMLA, selecione uma palavra-chave no Editor de Consultas XMLA e clique em **F1**.  
  
-   Para obter ajuda dinâmica sobre a sintaxe XMLA, no menu **Ajuda** , clique em **Ajuda Dinâmica** para abrir o componente da Ajuda Dinâmica. Com a Ajuda Dinâmica, os tópicos de ajuda aparecem na janela **Ajuda Dinâmica** quando são digitadas palavras-chave no Editor de Consultas.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra de ferramentas de Editores do SQL Server Analysis Services  
 Quando o Editor de Consultas XMLA está aberto, a barra de ferramentas dos **Editores do SQL Server Analysis Services** é exibida com os botões a seguir.  
  
|Termo|Definição|  
|----------|----------------|  
|**Connect**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Desligar**|Desconecta o Editor de Consultas XMLA de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Alterar conexão**|Abre a caixa de diálogo **Conectar ao Servidor** para estabelecer uma conexão com uma instância diferente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nova consulta com a conexão atual**|Abre uma nova janela do Editor de Consultas XMLA, utilizando as informações de conexão da janela atual do Editor de Consultas XMLA.|  
|**Bancos de dados disponíveis**|Altera a conexão para outro banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na mesma instância.|  
|**Executados**|Executa o código selecionado ou, se nenhum código for selecionado, esta opção executará todo o código no Editor de Consultas XMLA.|  
|**Passar**|Verifica a sintaxe do código selecionado. Se nenhum código for selecionado, essa opção verificará a sintaxe de toda a janela Editor de Consultas XMLA.|  
|**Cancelar execução de consulta**|Envia uma solicitação de cancelamento ao servidor. Algumas consultas não podem ser canceladas imediatamente, mas precisam esperar por uma condição de cancelamento satisfatória. Quando consultas são canceladas, podem ocorrer atrasos enquanto as transações são convertidas.|  
  
## <a name="xmla-query-editor-window"></a>Janela Editor de Consultas XMLA  
 As seguintes opções estão disponíveis no Editor de Consultas XMLA:  
  
|Termo|Definição|  
|----------|----------------|  
|**janela Editor de consultas**|Digite as instruções e os scripts XMLA a serem executados pelo Editor de Consultas XMLA.<br /><br /> O menu de contexto do editor de consultas fornece as seguintes opções:<br /><br /> **Recortar**: copia a seleção atual para a área de transferência e remove a seleção da janela do editor de consultas.<br />**Copiar**: copia a seleção atual para a área de transferência.<br />**Colar**: cola o conteúdo da área de transferência na seleção atual.<br />**Conectar**: abre a caixa de diálogo **conectar ao servidor** para estabelecer uma conexão com uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância do.<br />**Desconectar: desconecta**o editor de consultas atual de uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância.<br />**Desconectar todas as consultas: desconecta**todos os editores de consulta abertos.<br />**Alterar conexão**: abre a caixa de diálogo **conectar ao servidor** para estabelecer uma conexão com uma instância [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] diferente.<br />**Abrir servidor no Pesquisador de objetos**: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] abre a instância para a qual o editor de consultas atual está conectado no **pesquisador de objetos**.<br />**Execute**: executa o código selecionado ou, se nenhum código for selecionado, executa todo o código no editor de consultas atual.<br />**Janela Propriedades**: exibe a janela **Propriedades** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para a janela de consulta atual.<br />**Opções de consulta**: exibe a caixa de diálogo **Opções de consulta** .|  
|**Janela Resultados**|Exibe os resultados de uma instrução ou script XMLA em texto.|  
|**Janela Mensagens**|Exibe informações sobre como uma instrução ou script XMLA foi executado. Por exemplo, esta janela exibe todos os erros encontrados durante a execução ou o número de células recuperados depois da execução.|  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de consultas MDX &#40;Analysis Services de dados multidimensionais&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Editor de consultas DMX &#40;Analysis Services de mineração de dados&#41;](dmx-query-editor-analysis-services-data-mining.md)   
 [Editores de consulta e de texto &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Atalhos de teclado do SQL Server Management Studio](../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
