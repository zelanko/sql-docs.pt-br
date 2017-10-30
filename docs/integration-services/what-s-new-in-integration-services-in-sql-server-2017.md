---
title: O que &#39; s no Integration Services no SQL Server de 2017 | Microsoft Docs
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 63aba0f64bc63a3a86e5aa07245375938acdf6e4
ms.contentlocale: pt-br
ms.lasthandoff: 09/29/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>O que &#39; s no Integration Services no SQL Server de 2017
Este tópico descreve os recursos adicionados ou atualizados no [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

>   [!NOTE]
> SQL Server 2017 também inclui os recursos do SQL Server 2016 e os recursos adicionados em atualizações do SQL Server 2016. Para obter informações sobre os novos recursos do SSIS no SQL Server 2016, consulte [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="highlights-of-this-release"></a>Destaques desta versão

Aqui estão os novos recursos mais importantes do Integration Services no SQL Server 2017.

-   **Expansão**. Distribuir a execução de pacotes SSIS mais facilmente em vários computadores de trabalho e gerenciar execuções e funcionários de um único computador mestre. Para obter mais informações, consulte [Integration Services expansão](../integration-services/scale-out/integration-services-ssis-scale-out.md).

-   **Serviços de integração em Linux**. Execute pacotes SSIS em computadores Linux. Para obter mais informações, consulte [extrair, transformar e carregar dados em Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

-   **Melhorias de conectividade**. Conecte-se a feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online com os componentes atualizados do OData. 

## <a name="new-in-azure-data-factory"></a>Nova fábrica de dados do Azure

Com a visualização pública do Azure Data Factory versão 2 de setembro de 2017, agora você pode fazer as seguintes ações:
-   Implante pacotes no banco de dados do catálogo do SSIS (SSISDB) no banco de dados do SQL Azure.
-   Execute os pacotes implantados no Azure em tempo de execução de integração de SSIS do Azure, um componente do Azure Data Factory versão 2.

Para obter mais informações, consulte [comparar e deslocar cargas de trabalho de serviços de integração do SQL Server para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Esses novos recursos requerem o SQL Server Data Tools (SSDT) versão 17.2 ou posterior, mas não precisam de 2017 do SQL Server ou SQL Server 2016. Quando você implanta pacotes no Azure, o Assistente de implantação de pacote sempre atualiza os pacotes para o formato mais recente do pacote.

## <a name="new-in-the-azure-feature-pack"></a>Novo no Azure Feature Pack

Além dos aprimoramentos de conectividade no SQL Server, o Integration Services Feature Pack para Azure adicionou suporte para repositório Azure Data Lake. Para obter mais informações, consulte o postagem de blog [novo Azure recurso Pack versão fortalecendo ADLS conectividade](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/). Consulte também [Azure Feature Pack para o Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md).

## <a name="new-in-sql-server-data-tools-ssdt"></a>Novo no SQL Server Data Tools (SSDT)

Agora você pode desenvolver projetos do SSIS e pacotes destinados a versões do SQL Server 2012 por meio de 2017 em 2017 do Visual Studio ou no Visual Studio 2015. Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>No SSIS no SQL Server de 2017 RC1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Recursos novos e alterados em expansão para SSIS

-   Agora, há suporte para alta disponibilidade no Mestre de Scale Out. Você pode habilitar o AlwaysOn para SSISDB e configurar o Windows Server failover clustering para o servidor que hospeda o serviço de escala Out mestre. Ao aplicar essa alteração para escala Out mestre, você evitar um ponto único de falha e fornece alta disponibilidade para a implantação de expansão inteira.
-   O tratamento do failover dos logs de execução dos Trabalhos de Scale Out foi aprimorado. Os logs de execução são persistidos no disco local no caso do trabalho de fora de escala para inesperadamente. Posteriormente, quando o trabalho for reiniciado, recarrega os logs persistentes e continua a salvá-las em SSISDB.
-   O parâmetro *runincluster* do procedimento armazenado **[catalog].[create_execution]** foi renomeado como *runinscaleout*, a fim de obter consistência e legibilidade. Essa alteração de nome de parâmetro tem o seguinte impacto:
    -   Se você tiver scripts existentes para executar pacotes em expansão, você precisa alterar o nome do parâmetro de *runincluster* para *runinscaleout* para fazer com que os scripts de trabalho no RC1.
    -   SQL Server Management Studio (SSMS) 17.1 e versões anteriores não é possível disparar a execução do pacote de expansão no RC1. A mensagem de erro é: "*@runincluster* não é um parâmetro para o procedimento **create_execution**." Esse problema é corrigido na próxima versão do SSMS, a versão 17.2. Versão mais recente do SSMS e 17.2 oferecem suporte a nova execução de pacote e o nome de parâmetro em expansão. Até que o SSMS versão 17.2 estiver disponível, como alternativa, você pode usar a versão existente do SSMS para gerar o script de execução do pacote e altere o nome do *runincluster* parâmetro *runinscaleout* no script e execute o script.
-   O catálogo do SSIS tem uma nova propriedade global para especificar o modo padrão de execução de pacotes do SSIS. Essa nova propriedade se aplica quando você chamar o **[catalog]. [ create_execution]** armazenado procedimento com o *runinscaleout* parâmetro definido como nulo. Este modo também se aplica a trabalhos do SQL Agent do SSIS. Você pode definir a propriedade global novo na caixa de diálogo de propriedades para o nó SSISDB no SSMS, ou com o seguinte comando:
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>No SSIS no SQL Server de 2017 CTP 2.1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Recursos novos e alterados em expansão para SSIS

-   Agora você pode usar o **Use32BitRuntime** parâmetro quando você acionar a execução em expansão.
-   Melhorou o desempenho de registro em log para SSISDB para execuções de pacote de expansão. Os logs de mensagem de evento e o contexto da mensagem agora são gravados SSISDB em modo de lote em vez de uma. Aqui estão algumas observações adicionais sobre esse aprimoramento:        
    - Alguns relatórios na versão atual do SQL Server Management Studio (SSMS) atualmente não exibir esses logs para execuções em expansão. Estimamos que eles terão suporte na próxima versão do SSMS. Os relatórios afetados incluem o *todas as conexões* relatório, o *contexto do erro* relatório e o *informações de Conexão* seção no painel de serviços de integração.
    - Uma nova coluna **event_message_guid** foi adicionado. Use essa coluna para unir [catalog]. exibição [event_message_context] e [catalog]. Exibir [event_messages] em vez de usar **event_message_id** quando você consulta esses registros de execuções em expansão.
-   Para obter o aplicativo de gerenciamento para SSIS expansão, [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17,1 ou posterior.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>No SSIS no SQL Server de 2017 CTP 2.0

Não há nenhum recurso novo do SSIS no SQL Server de 2017 CTP 2.0.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>No SSIS no SQL Server de 2017 CTP 1.4

Não há nenhum recurso novo do SSIS no SQL Server 2017 CTP 1.4.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>No SSIS no SQL Server de 2017 CTP 1.3

Não há nenhum recurso novo do SSIS no SQL Server de 2017 CTP 1.3.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>No SSIS no SQL Server de 2017 CTP 1.2

Não há nenhum recurso novo do SSIS no SQL Server de 2017 CTP 1.2.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>No SSIS no SQL Server de 2017 CTP 1.1

Não há nenhum recurso novo do SSIS no SQL Server de 2017 CTP 1.1.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>No SSIS no SQL Server de 2017 CTP 1.0

### <a name="scale-out-for-ssis"></a>Expansão para o SSIS

O recurso de Expansão torna muito mais fácil executar [!INCLUDE[ssIS_md](../includes/ssis-md.md)] em vários computadores. 
   
Após a instalação do Mestre de Expansão e do Trabalho de Expansão, o pacote pode ser distribuído para executar diferentes Trabalhos automaticamente. Se a execução for finalizada inesperadamente, a execução será repetida automaticamente. Além disso, todas as execuções e Trabalhos podem ser gerenciados de forma centralizada usando o Mestre.
   
Para obter mais informações, consulte [Expansão do Integration Services](../integration-services/scale-out/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Suporte para recursos Online do Microsoft Dynamics

O Gerenciador de Fontes OData e o Gerenciador de Conexões OData agora têm suporte para conexão aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.


