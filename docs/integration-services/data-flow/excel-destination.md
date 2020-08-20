---
description: Destino do Excel
title: Destino do Excel | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2abf3c8a09ead6369a5201a2d582623f05bc2f79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477833"
---
# <a name="excel-destination"></a>Destino do Excel

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O destino do Excel carrega dados em planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).
  
## <a name="access-modes"></a>Modos de acesso  
 O destino do Excel fornece três modos de acesso diferentes para carregar dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
## <a name="configure-the-excel-destination"></a>Configurar o destino do Excel  
 O destino do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo de pasta de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 O destino do Excel tem uma entrada regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Editor de Destinos do Excel (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos do Excel** para especificar informações da fonte de dados e visualizar os resultados. O destino do Excel carrega dados em uma planilha ou um intervalo nomeado em uma pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** do destino do Excel não está disponível no **Editor de Destinos do Excel**, mas pode ser definida com o **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Destino do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do Excel**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma planilha ou intervalo nomeado na fonte de dados do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Carregue dados no destino do Excel usando uma consulta SQL.|  
  
 **Nome da planilha do Excel**  
 Selecione o destino do Excel da listagem suspensa. Se a lista estiver vazia, clique em **Novo**.  
  
 **Novo**  
 Clique em **Novo** para iniciar a caixa de diálogo **Criar Tabela** . Quando você clicar em **OK**, a caixa de diálogo cria o arquivo Excel para o qual o **Gerenciador de Conexões do Excel** aponta.  
  
 **Exibir dados existentes**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na fonte de dados.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Construir Consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar Consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="excel-destination-editor-mappings-page"></a>Editor de Destino do Excel (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo do **Editor de Destinos do Excel** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. É possível alterar os mapeamentos usando a lista **Colunas de Entrada Disponíveis**.  
  
 **Coluna de Destino**  
 Exiba cada coluna de destino disponível, seja ela mapeada ou não.  
  
## <a name="excel-destination-editor-error-output-page"></a>Editor de Destino do Excel (página Saída de Erro)
  Use a página **Avançado** da caixa de diálogo **Editor de Destinos do Excel** para especificar opções de tratamento de erro.  
  
### <a name="options"></a>Opções  
 **Entrada ou Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Veja as colunas externas (origem) que você selecionou no nó **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
 [Origem do Excel](../../integration-services/data-flow/excel-source.md)   
[Gerenciador de Conexões do Excel](../connection-manager/excel-connection-manager.md)
