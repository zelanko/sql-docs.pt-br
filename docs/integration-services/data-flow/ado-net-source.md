---
title: Origem do ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ca0a56e3168e5493104cd54472516800d444078
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665570"
---
# <a name="ado-net-source"></a>Origem do ADO NET
  A origem do ADO NET recebe dados de um provedor de .NET e os disponibiliza para o fluxo de dados.  
  
 Você pode usar a fonte ADO.NET para se conectar ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Não há suporte para a conexão ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] com o uso do OLE DB. Para obter mais informações sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], consulte [Diretrizes gerais e limitações (Banco de dados SQL do Microsoft Azure)](http://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 A fonte converte qualquer tipo de dados que não é mapeado para um tipo de dados específico do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um tipo de dados DT_NTEXT do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Essa conversão ocorre mesmo que o tipo de dados seja **System.Object**.  
  
 É possível alterar o tipo de dados DT_NTEXT para o tipo de dados DT_WSTR ou alterar DT_WSTR para DT_NTEXT. Para alterar tipos de dados, defina a propriedade **DataType** na caixa de diálogo **Editor Avançado** da fonte ADO.NET. Para obter mais informações, consulte [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 O tipo de dados DT_NTEXT também pode ser convertido no tipo de dados DT_BYTES ou DT_STR usando uma transformação Conversão de Dados depois da origem do ADO NET. Para obter mais informações, consulte [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
 No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os tipos de dados de data, DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, são mapeados para certos tipos de dados de data no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode configurar a fonte ADO.NET para converter os tipos de dados de data usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] naqueles usados pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para configurar a fonte ADO.NET para converter esses tipos de dados de data, defina a propriedade **Versão do Sistema de Tipos** do gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] como **Mais Recente**. (A propriedade **Versão do Sistema de Tipos** está localizada na página **Tudo** da caixa de diálogo **Gerenciador de Conexões** . Para abrir a caixa de diálogo **Gerenciador de Conexões** , clique com o botão direito do mouse no gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e clique em **Editar**.)  
  
> [!NOTE]  
>  Se a propriedade **Versão do Sistema de Tipos** do gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] for definida como **SQL Server 2005**, o sistema converterá os tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em DT_WSTR.  
  
 O sistema converte UDTs (tipos de dados definidos pelo usuário) em BLOBs (objetos grandes binários) do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando o gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] especifica o provedor como o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient). O sistema aplica as regras a seguir ao converter o tipo de dados UDT:  
  
-   Se os dados forem UDTs pequenos, o sistema converterá os dados em DT_BYTES.  
  
-   Se os dados forem UDTs que não são grandes e a propriedade **Length** da coluna do banco de dados for definida como -1 ou um valor superior a 8.000 bytes, o sistema converterá os dados em DT_IMAGE.  
  
-   Se os dados forem UDTs grandes, o sistema converterá os dados em DT_IMAGE.  
  
    > [!NOTE]  
    >  Se a origem do ADO NET não estiver configurada para usar a saída de erro, o sistema enviará os dados para a coluna DT_IMAGE em blocos de 8.000 bytes. Se a origem do ADO NET for configurada para usar a saída de erro, o sistema passará a matriz inteira de bytes para a coluna DT_IMAGE. Para obter mais informações sobre como configurar componentes para usar a saída de erro, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Para obter mais informações sobre os tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , as conversões de tipos de dados com suporte e o mapeamento de tipos de dados em alguns bancos de dados, incluindo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Para obter informações sobre como mapear tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em tipos de dados gerenciados, consulte [Trabalhando com tipos de dados no fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Solução de problemas da origem do ADO NET  
 Você pode registrar as chamadas que a origem do ADO NET faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem do ADO NET executa. Para registrar as chamadas que a fonte ADO.NET faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível do pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>Configuração da origem do ADO NET  
 Para configurar a origem do ADO NET, forneça a instrução SQL que define o conjunto de resultados. Por exemplo, a fonte ADO.NET que se conecta ao banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] e que usa a instrução SQL `SELECT * FROM Production.Product` extrai todas as linhas da tabela **Production.Product** e fornece o conjunto de dados para um componente de downstream.  
  
> [!NOTE]  
>  Quando você usa uma instrução SQL para invocar um procedimento armazenado que retorna resultados de uma tabela temporária, use a opção de WITH RESULT SETS para definir metadados para o conjunto de resultados.  
  
> [!NOTE]  
>  Se você usar uma instrução SQL para executar um procedimento armazenado e o pacote falhar com o erro a seguir, você poderá resolver o erro adicionando a instrução **SET FMTONLY OFF** antes da instrução exec.  
>   
>  **Não é possível encontrar a coluna <nome_da_coluna> na fonte de dados.**  
  
 A fonte ADO.NET usa um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para se conectar a uma fonte de dados, e o gerenciador de conexões especifica o provedor .NET. Para obter mais informações, consulte [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 A origem do ADO NET tem uma saída regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>Editor de origem ADO NET (Página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** para selecionar o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Gerenciador de Conexões**.  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões ADO.NET**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões ADO NET** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou visualize na fonte de dados [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .|  
|Comando SQL|Recupere os dados da fonte de dados [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usando uma consulta SQL.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, o valor \<valor muito grande para ser exibido> ou System.Byte[] é exibido. O primeiro é exibido quando a fonte de dados é acessada usando o provedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , o último ao usar o provedor Native Client do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
## <a name="ado-net-source-editor-columns-page"></a>Editor de Origem ADO NET (Página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem ADO NET** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir a página Colunas**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Colunas**.  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas.  
  
 **Coluna Externa**  
 Exiba as colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados dessa origem.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome fornecido será exibido no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="ado-net-source-editor-error-output-page"></a>Editor de Origem ADO NET (Página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ADO NET** para selecionar as opções de manipulação de erros e definir as propriedades nas colunas de saída de erros.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Saída de Erro**.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** .  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Destino DataReader](../../integration-services/data-flow/datareader-destination.md)   
 [Destino do ADO NET](../../integration-services/data-flow/ado-net-destination.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
