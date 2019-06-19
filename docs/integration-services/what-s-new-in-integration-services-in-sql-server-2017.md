---
title: Novidades do Integration Services no SQL Server 2017 | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6d8660aa65699e6abd22c73e13c3673903ff6bfb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65713542"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>Novidades do Integration Services no SQL Server 2017

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tópico descreve os recursos adicionados ou atualizados no [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

> [!NOTE]
> O SQL Server 2017 também inclui os recursos do SQL Server 2016 e os recursos adicionados nas atualizações do SQL Server 2016. Para obter informações sobre os novos recursos do SSIS no SQL Server 2016, consulte [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="highlights-of-this-release"></a>Destaques desta versão

Veja abaixo os novos recursos mais importantes do Integration Services no SQL Server 2017.

-   **Scale Out**. Distribua a execução de pacotes do SSIS com mais facilidade em vários computadores de trabalho e gerencie execuções e trabalhos em um único computador mestre. Para obter mais informações, consulte [Integration Services Scale Out](../integration-services/scale-out/integration-services-ssis-scale-out.md).

-   **Integration Services no Linux**. Execute pacotes do SSIS em computadores Linux. Para obter mais informações, consulte [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

-   **Melhorias de conectividade**. Conecte-se a feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online com os componentes atualizados do OData. 

## <a name="new-in-azure-data-factory"></a>Novidades do Azure Data Factory

Com a visualização pública do Azure Data Factory versão 2 em setembro de 2017, agora você pode fazer o seguinte:
-   Implantar pacotes no SSISDB (banco de dados do Catálogo do SSIS) no Banco de Dados SQL do Azure.
-   Execute os pacotes implantados no Azure no Azure-SSIS Integration Runtime, um componente do Azure Data Factory versão 2.

Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Essas novas funcionalidades exigem o SSDT (SQL Server Data Tools) versão 17.2 ou posterior, mas não exigem o SQL Server 2017 nem o SQL Server 2016. Quando você implanta pacotes no Azure, o Assistente de Implantação de Pacotes sempre faz upgrade dos pacotes para o formato de pacote mais recente.

## <a name="new-in-the-azure-feature-pack"></a>Novidades do Feature pack do Azure

Além das melhorias de conectividade no SQL Server, o Feature Pack do Integration Services para Azure adicionou suporte para o Azure Data Lake Store. Para obter mais informações, consulte o postagem no blog [Nova versão do feature pack do Azure fortalecendo a conectividade ADLS](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/). Consulte também [Feature pack do Azure para o SSIS (Integration Services)](azure-feature-pack-for-integration-services-ssis.md).

## <a name="new-in-sql-server-data-tools-ssdt"></a>Novidades do SSDT (SQL Server Data Tools)

Agora você pode desenvolver projetos e pacotes do SSIS destinados ao SQL Server versões 2012 a 2017 no Visual Studio 2017 ou Visual Studio 2015. Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>Novidades do SSIS no SQL Server 2017 RC1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Recursos novos e alterados no Scale Out para SSIS

-   Agora, há suporte para alta disponibilidade no Mestre de Scale Out. Habilite o Always On para o SSISDB e configure o clustering de failover do Windows Server para o servidor que hospeda o serviço Mestre do Scale Out. Aplicando essa alteração ao Mestre do Scale Out, você evita um ponto único de falha e fornece alta disponibilidade para toda a implantação do Scale Out.
-   O tratamento do failover dos logs de execução dos Trabalhos de Scale Out foi aprimorado. Os logs de execução são persistidos no disco local caso o Trabalho do Scale Out seja interrompido inesperadamente. Posteriormente, quando o trabalho for reiniciado, ele recarregará os logs persistentes e continuará salvando-os no SSISDB.
-   O parâmetro *runincluster* do procedimento armazenado **[catalog].[create_execution]** foi renomeado como *runinscaleout*, a fim de obter consistência e legibilidade. Essa alteração de nome de parâmetro tem o seguinte impacto:
    -   Se você tiver scripts existentes para executar pacotes no Scale Out, precisará alterar o nome do parâmetro de *runincluster* para *runinscaleout* para que os scripts funcionem no RC1.
    -   O SSMS (SQL Server Management Studio) 17.1 e versões anteriores não pode disparar a execução de pacote no Scale Out no RC1. A mensagem de erro é: " *@runincluster* não é um parâmetro para o procedimento **create_execution**." Esse problema é corrigido na próxima versão do SSMS, a versão 17.2. A versão 17.2 e posterior do SSMS dão suporte ao novo nome de parâmetro e execução de pacote no Scale Out. Até que o SSMS versão 17.2 esteja disponível, como solução alternativa, é possível usar a versão existente do SSMS para gerar o script de execução do pacote e, em seguida, alterar o nome do parâmetro *runincluster* para *runinscaleout* no script e executá-lo.
-   O catálogo do SSIS tem uma nova propriedade global para especificar o modo padrão de execução de pacotes do SSIS. Essa nova propriedade se aplica quando você chama o procedimento armazenado **[catalog].[create_execution]** com o parâmetro *runinscaleout* definido como nulo. Esse modo também se aplica a trabalhos do SQL Agent do SSIS. Defina a nova propriedade global na caixa de diálogo Propriedades do nó do SSISDB no SSMS ou com o seguinte comando:
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>Novidades do SSIS no SQL Server 2017 CTP 2.1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Recursos novos e alterados no Scale Out para SSIS

-   Agora você pode usar o parâmetro **Use32BitRuntime** ao disparar a execução no Scale Out.
-   O desempenho do log no SSISDB para execuções de pacote no Scale Out foi aprimorado. Os logs de Mensagem do Evento e Contexto da Mensagem agora são gravados no SSISDB no modo de lote em vez de individualmente. Estas são algumas observações adicionais sobre essa melhoria:        
    - Alguns relatórios na versão atual do SSMS (SQL Server Management Studio) atualmente não exibem esses logs para execuções no Scale Out. A previsão é que eles terão suporte na próxima versão do SSMS. Os relatórios afetados incluem o relatório *Todas as Conexões*, o relatório *Contexto do Erro* e a seção *Informações de Conexão* no Painel do Integration Services.
    - Uma nova coluna **event_message_guid** foi adicionada. Use essa coluna para unir as exibições [catalog].[event_message_context] e [catalog].[event_messages] em vez de usar **event_message_id** ao consultar esses logs de execuções no Scale Out.
-   Para obter o aplicativo de gerenciamento para o SSIS Scale Out, [baixe o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 ou posterior.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>Novidades do SSIS no SQL Server 2017 CTP 2.0

Não há novos recursos do SSIS no SQL Server 2017 CTP 2.0.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>Novidades do SSIS no SQL Server 2017 CTP 1.4

Não há novos recursos do SSIS no SQL Server 2017 CTP 1.4.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>Novidades do SSIS no SQL Server 2017 CTP 1.3

Não há novos recursos do SSIS no SQL Server 2017 CTP 1.3.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>Novidades do SSIS no SQL Server 2017 CTP 1.2

Não há novos recursos do SSIS no SQL Server 2017 CTP 1.2.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>Novidades do SSIS no SQL Server 2017 CTP 1.1

Não há novos recursos do SSIS no SQL Server 2017 CTP 1.1.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>Novidades do SSIS no SQL Server 2017 CTP 1.0

### <a name="scale-out-for-ssis"></a>Expansão para o SSIS

O recurso de Expansão torna muito mais fácil executar [!INCLUDE[ssIS_md](../includes/ssis-md.md)] em vários computadores. 
   
Após a instalação do Mestre de Expansão e do Trabalho de Expansão, o pacote pode ser distribuído para executar diferentes Trabalhos automaticamente. Se a execução for finalizada inesperadamente, a execução será repetida automaticamente. Além disso, todas as execuções e Trabalhos podem ser gerenciados de forma centralizada usando o Mestre.
   
Para obter mais informações, consulte [Expansão do Integration Services](../integration-services/scale-out/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Suporte para recursos Online do Microsoft Dynamics

O Gerenciador de Fontes OData e o Gerenciador de Conexões OData agora têm suporte para conexão aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.

