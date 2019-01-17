---
title: Destino do ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetdest.f1
- sql13.dts.designer.adonetdest.connection.f1
- sql13.dts.designer.adonetdest.mappings.f1
- sql13.dts.designer.adonetdest.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a462e54379a5a916d6b302f99ef6f44d2148399a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209085"
---
# <a name="ado-net-destination"></a>Destino do ADO NET
  O destino ADO NET carrega dados em uma variedade de bancos de dados compatíveis com o [!INCLUDE[vstecado](../../includes/vstecado-md.md)]que utilizam uma tabela ou exibição de banco de dados. Você tem a opção de carregar esses dados em uma tabela ou exibição existente ou de criar uma nova tabela e carregar os dados nessa tabela.  
  
 Você pode usar o destino do ADO NET para conectar-se ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Não há suporte para a conexão ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] com o uso do OLE DB. Para obter mais informações sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], consulte [Diretrizes gerais e limitações (Banco de dados SQL do Microsoft Azure)](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="troubleshooting-the-ado-net-destination"></a>Solucionando problemas do destino ADO NET  
 Você pode registrar as chamadas que o destino ADO NET faz para provedores de dados externos. É possível usar essa capacidade de registro para solucionar o problema de salvar os dados em fontes de dados externas que o destino ADO NET executa. Para registrar as chamadas que o destino ADO NET faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacotes. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ado-net-destination"></a>Configurando o destino ADO NET  
 Esse destino usa um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para conectar-se a uma fonte de dados e o gerenciador de conexões especifica o provedor do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a ser usado. Para obter mais informações, consulte [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 Um destino ADO NET inclui mapeamentos entre as colunas de entrada e as colunas da fonte de dados de destino. Você não precisa mapear colunas de entrada para todas as colunas de destino. No entanto, as propriedades de algumas colunas de destino podem precisar do mapeamento de colunas de entrada. Caso contrário, podem ocorrer erros. Por exemplo, se uma coluna de destino não permitir valores nulos, você deve mapear uma coluna de entrada para aquela coluna de destino. Além disso, os tipos de dados de colunas mapeadas devem ser compatíveis. Por exemplo, você não poderá mapear uma coluna de entrada com um tipo de dados String para uma coluna de destino com um tipo de dados numéricos se o provedor do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] não der suporte a este mapeamento.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte à inserção de texto em colunas cujo tipo de dados é definido como imagem. Para obter mais informações sobre os tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
>  O destino ADO NET não dá suporte ao mapeamento de uma coluna de entrada cujo tipo é definido como DT_DBTIME para uma coluna de banco de dados cujo tipo é definido como data e hora. Para obter mais informações sobre tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Tipos de Dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 O destino ADO NET tem uma entrada regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-destination-editor-connection-manager-page"></a>Editor de Destino ADO NET (Página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino ADO NET** para selecionar a conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha o destino ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino ADO NET.  
  
3.  No **Editor de Destino ADO NET**, clique em **Gerenciador de Conexões**.  
  
### <a name="static-options"></a>Opções estáticas  
 **Connection manager**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões ADO NET** .  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova tabela clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova tabela ou exibição usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
 **Use a inserção em massa quando disponível**  
 Especifique se a interface <xref:System.Data.SqlClient.SqlBulkCopy> deve ser usada para melhorar o desempenho de operações de inserção em massa.  
  
 Somente os provedores ADO.NET que retornam um objeto <xref:System.Data.SqlClient.SqlConnection> dão suporte ao uso da interface <xref:System.Data.SqlClient.SqlBulkCopy> . O .NET Data Provider for SQL Server (SqlClient) retorna um objeto <xref:System.Data.SqlClient.SqlConnection> e um provedor personalizado pode retornar um objeto <xref:System.Data.SqlClient.SqlConnection> .  
  
 Você pode usar o Provedor de Dados .NET para o SQL Server (SqlClient) para conectar-se ao [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 Se você selecionar **Usar a inserção em massa quando disponível**e definir a opção **Erro** como **Redirecionar a linha**, o lote de dados que o destino redireciona à saída de erro poderá incluir linhas válidas. Para obter mais informações sobre o tratamento de erro em operações em massa, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md). Para obter mais informações sobre a opção **Erro** , consulte [Editor de Destino ADO NET &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]
>  Se uma tabela de origem do SQL Server ou do Sybase incluir uma coluna de identidade, utilize as tarefas Executar SQL para habilitar IDENTITY_INSERT antes do destino ADO NET e desabilitá-lo novamente depois. (A propriedade da coluna de identidade especifica um valor incremental para a coluna. A instrução SET IDENTITY_INSERT permite inserir valores explícitos da tabela de origem na coluna de identidade na tabela de destino.)  
> 
>   Para executar com êxito as instruções SET IDENTITY_INSERT e o carregamento de dados, você precisa fazer o descrito a seguir.  
>       1. Use o mesmo gerenciador de conexões ADO.NET para as tarefas Executar SQL e para o destino ADO NET.  
>       2. No gerenciador de conexões, defina as propriedades **RetainSameConnection** e **MultipleActiveResultSets** como True.  
>       3. No destino ADO.NET, defina a propriedade **UseBulkInsertWhenPossible** como False.   
> 
>  Para obter mais informações, consulte [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) e [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md).  
  
## <a name="external-resources"></a>Recursos externos  
 Artigo técnico sobre o [Loading data to Windows Azure SQL Database the fast way](https://go.microsoft.com/fwlink/?LinkId=244333)(Carregando dados no Banco de Dados SQL do Microsoft Azure), em sqlcat.com  
  
## <a name="ado-net-destination-editor-mappings-page"></a>Editor de Destino ADO NET (Página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino ADO NET** para mapear as colunas de entrada nas colunas de destino.  
  
 **Para abrir a página Mapeamentos**  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha o destino ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino ADO NET.  
  
3.  No **Editor de Destino ADO NET**, clique em **Mapeamentos**.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exiba as colunas de entrada que você selecionou. Você pode remover mapeamentos selecionando **\<ignorar>** para excluir colunas da saída.  
  
 **Coluna de Destino**  
 Visualize cada coluna de destino disponível, esteja ela mapeada ou não.  
  
## <a name="ado-net-destination-editor-error-output-page"></a>Editor de Destino ADO NET (Página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino ADO NET** para especificar as opções para tratamento de erros.  
  
 **Para abrir a página Saída de Erro**  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha o destino ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino ADO NET.  
  
3.  No **Editor de Destino ADO NET**, clique em **Saída de Erro**.  
  
### <a name="options"></a>Opções  
 **Entrada ou Saída**  
 Visualize o nome da entrada.  
  
 **Coluna**  
 Não usado.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Não usado.  
  
 **Descrição**  
 Visualize a descrição da operação.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
  
