---
title: Origem do ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 296163b64d565ae3a65a16f1dbbf002bfc464bee
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153965"
---
# <a name="ado-net-source"></a>Origem do ADO NET
  A origem do ADO NET recebe dados de um provedor de .NET e os disponibiliza para o fluxo de dados.  
  
 Você pode usar a fonte ADO.NET para se conectar ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Não há suporte para a conexão ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] com o uso do OLE DB. Para obter mais informações [!INCLUDE[ssSDS](../../includes/sssds-md.md)]sobre o, consulte [diretrizes gerais e limitações (banco de dados SQL do Azure)](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 A fonte converte qualquer tipo de dados que não é mapeado para um tipo de dados específico do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um tipo de dados DT_NTEXT do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Essa conversão ocorre mesmo que o tipo de dados seja `System.Object`.  
  
 É possível alterar o tipo de dados DT_NTEXT para o tipo de dados DT_WSTR ou alterar DT_WSTR para DT_NTEXT. Para alterar tipos de dados, defina a propriedade **DataType** na caixa de diálogo **Editor Avançado** da fonte ADO.NET. Para obter mais informações, consulte [Propriedades comuns](../common-properties.md).  
  
 O tipo de dados DT_NTEXT também pode ser convertido no tipo de dados DT_BYTES ou DT_STR usando uma transformação Conversão de Dados depois da origem do ADO NET. Para obter mais informações, consulte [Data Conversion Transformation](transformations/data-conversion-transformation.md).  
  
 No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], os tipos de dados de data, DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, são mapeados para certos tipos de dados de data no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode configurar a fonte ADO.NET para converter os tipos de dados de data usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] naqueles usados pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para configurar a fonte ADO.NET para converter esses tipos de dados de data, defina a propriedade **Versão do Sistema de Tipos** do gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] como **Mais Recente**. (A propriedade **Versão do Sistema de Tipos** está localizada na página **Tudo** da caixa de diálogo **Gerenciador de Conexões** . Para abrir a caixa de diálogo **Gerenciador de Conexões** , clique com o botão direito do mouse no gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e clique em **Editar**.)  
  
> [!NOTE]  
>  Se a propriedade **Versão do Sistema de Tipos** do gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] for definida como **SQL Server 2005**, o sistema converterá os tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em DT_WSTR.  
  
 O sistema converte UDTs (tipos de dados definidos pelo usuário) em BLOBs (objetos grandes binários) do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando o gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] especifica o provedor como o Provedor de Dados .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient). O sistema aplica as regras a seguir ao converter o tipo de dados UDT:  
  
-   Se os dados forem UDTs pequenos, o sistema converterá os dados em DT_BYTES.  
  
-   Se os dados forem UDTs que não são grandes e a propriedade **Length** da coluna do banco de dados for definida como -1 ou um valor superior a 8.000 bytes, o sistema converterá os dados em DT_IMAGE.  
  
-   Se os dados forem UDTs grandes, o sistema converterá os dados em DT_IMAGE.  
  
    > [!NOTE]  
    >  Se a origem do ADO NET não estiver configurada para usar a saída de erro, o sistema enviará os dados para a coluna DT_IMAGE em blocos de 8.000 bytes. Se a origem do ADO NET for configurada para usar a saída de erro, o sistema passará a matriz inteira de bytes para a coluna DT_IMAGE. Para obter mais informações sobre como configurar componentes para usar a saída de erro, consulte [Tratamento de erros em dados](error-handling-in-data.md).  
  
 Para obter mais informações sobre os tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , as conversões de tipos de dados com suporte e o mapeamento de tipos de dados em alguns bancos de dados, incluindo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Tipos de dados do Integration Services](integration-services-data-types.md).  
  
 Para obter informações sobre como mapear tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em tipos de dados gerenciados, consulte [Trabalhando com tipos de dados no fluxo de dados](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Solução de problemas da origem do ADO NET  
 Você pode registrar as chamadas que a origem do ADO NET faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem do ADO NET executa. Para registrar as chamadas que a fonte ADO.NET faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível do pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>Configuração da origem do ADO NET  
 Para configurar a origem do ADO NET, forneça a instrução SQL que define o conjunto de resultados. Por exemplo, a fonte ADO.NET que se conecta ao banco de dados [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] e que usa a instrução SQL `SELECT * FROM Production.Product` extrai todas as linhas da tabela **Production.Product** e fornece o conjunto de dados para um componente de downstream.  
  
> [!NOTE]  
>  Quando você usa uma instrução SQL para invocar um procedimento armazenado que retorna resultados de uma tabela temporária, use a opção de WITH RESULT SETS para definir metadados para o conjunto de resultados.  
  
> [!NOTE]  
>  Se você usar uma instrução SQL para executar um procedimento armazenado e o pacote falhar com o seguinte erro, você poderá resolver o erro adicionando a instrução `SET FMTONLY OFF` antes da instrução exec.  
>   
>  **Não é possível encontrar a coluna <nome_da_coluna> na fonte de dados.**  
  
 A fonte ADO.NET usa um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para se conectar a uma fonte de dados, e o gerenciador de conexões especifica o provedor .NET. Para obter mais informações, consulte [Gerenciador de conexões ADO.NET](../connection-manager/ado-net-connection-manager.md).  
  
 A origem do ADO NET tem uma saída regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do ADO NET](ado-net-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Destino DataReader](datareader-destination.md)   
 [Destino do ADO NET](ado-net-destination.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
