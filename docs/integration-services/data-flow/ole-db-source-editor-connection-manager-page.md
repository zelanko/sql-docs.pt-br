---
title: "Editor de origem OLE DB (página Gerenciador de Conexão) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f996b8e5fd5d361959a1c972718b730896a2d805
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="ole-db-source-editor-connection-manager-page"></a>Editor de Origem OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem OLE DB** para selecionar o gerenciador de conexões OLE DB para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, use uma origem OLE DB. Você não pode usar uma origem do Excel para carregar dados de uma fonte de dados do Excel 2007. Para obter mais informações, consulte [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 ou uma versão anterior, use uma origem do Excel. Para obter mais informações, consulte [Editor de Fonte Excel &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** da origem OLE DB não está disponível no **Editor de Origem OLE DB**, mas pode ser definida usando o **Editor Avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Propriedades personalizadas do OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
 Para saber mais sobre a origem de OLE DB, consulte [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Abrir a página do Gerenciador de Conexões do Editor de Origem OLE DB  
  
1.  Adicione a origem OLE DB ao pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente de origem e clique em **Editar**.  
  
3.  Clique em **Gerenciador de Conexões**.  
  
## <a name="static-options"></a>Opções estáticas  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou exibição na fonte de dados OLE DB.|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Recupere os dados da fonte de dados OLE DB usando uma consulta SQL.|  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, os valores de \<valor muito grande para ser exibida > ou System. Byte []. O primeiro é exibido quando a fonte de dados é acessada usando o provedor SQL OLE DB e o segundo, usando o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parâmetros**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Build query**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origem OLE DB &#40; Página colunas &#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)   
 [Editor de origem OLE DB &#40; Página de saída de erro &#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)   
 [Extrair dados por meio da origem OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)   
 [Gerenciador de Conexão do OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  
