---
title: Origem CDC | Microsoft Docs
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
- sql13.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 031c5321bc17307a12403d974380eb710c841653
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source"></a>Origem CDC
  A origem CDC lê um intervalo de dados de alteração de tabelas de alteração do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e entrega o downstream de alterações a outros SSIS componentes.  
  
 O intervalo de leitura de dados de alteração pela origem CDC é chamado Intervalo de Processamento CDC e é determinado pela tarefa Controle de CDC que é executada antes do início do fluxo de dados atual. O Intervalo de Processamento CDC é derivado do valor de uma variável de pacote que mantém o estado do processamento CDC para um grupo de tabelas.  
  
 A origem CDC extrai dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma tabela de banco de dados, uma exibição ou uma instrução SQL.  
  
 A origem CDC usa as configurações seguintes:  
  
-   Um gerenciador de conexões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET para acessar o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Para obter mais informações sobre como configurar a conexão de origem CDC, consulte [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).  
  
-   Uma tabela habilitada para CDC.  
  
-   O nome da instância de captura da tabela selecionada (se houver mais de uma).  
  
-   O modo de processamento de alteração.  
  
-   O nome da variável de pacote do estado CDC com base no qual o intervalo de Processamento CDC é determinado. A origem CDC não modifica essa variável.  
  
 Os dados retornados pela origem CDC são o mesmo que o retornado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções CDC **fn_cdc_get_all_changes _\<nome da instância de captura >** ou **fn_cdc_get_net_changes _\<nome da instância de captura >** (quando disponível). A única adição opcional é a coluna, **__$initial_processing** , que indica se o intervalo de processamento atual pode se sobrepor a uma carga inicial da tabela. Para obter mais informações sobre o processamento inicial, consulte [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 A origem CDC tem uma saída regular e uma saída de erro.  
  
## <a name="error-handling"></a>Tratamento de erros  
 A origem CDC tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: o valor sempre é -1.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   **Colunas de Linha de Erro**: os dados de registro que causam o erro.  
  
 Dependendo da configuração de comportamento de erro, a origem CDC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro. Para obter mais informações, consulte [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md).  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 O componente origem CDC para Microsoft oferece suporte a todos os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão mapeados para os tipos de dados SSIS corretos.  
  
## <a name="troubleshooting-the-cdc-source"></a>Solucionando problemas da origem CDC  
 A seguir são apresentadas informações sobre como solucionar problemas de origem CDC.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>Use este script para isolar problemas e reproduzi-los no SQL Server Management Studio  
 Uma operação de origem CDC é governada pela operação da tarefa Controle CDC executada antes da chamada à origem CDC. A tarefa Controle CDC prepara o valor da variável de pacote do estado CDC para conter LSNs de início e término. Ela executa uma função equivalente ao seguinte script:  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 onde:  
  
-   \<CDC-habilitado-database-name > é o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados que contém as tabelas de alteração.  
  
-   \<valor-from-state-cs > é o valor que aparece na variável de estado de CDC, como em CS /\<valor-from-state-cs > / (CS significa Current-processamento--início do intervalo).  
  
-   \<valor de estado ce > é o valor que aparece na variável de estado de CDC, como em CE /\<valor-from-state-cs > / (CE significa Current-processamento--fim do intervalo).  
  
-   \<modo > são os modos de processamento CDC. Os modos de processamento têm um dos seguintes valores: **Tudo**, **Tudo com Valores Antigos**, **Rede**, **Rede com Máscara de Atualização**, **Rede com Mesclagem**.  
  
 Este script ajuda a isolar problemas reproduzindo-os no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], onde é fácil reproduzir e identificar erros.  
  
#### <a name="sql-server-error-message"></a>Mensagem de erro do SQL Server  
 A mensagem seguinte poderá ser retornada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 **Um número insuficiente de argumentos foi fornecido para o procedimento ou função CDC. fn_cdc_get_net_changes_\<... >.**  
  
 Esse erro não indica que um argumento está faltando. Significa que os valores de LSN de início ou fim na variável de estado CDC são inválidos.  
  
## <a name="configuring-the-cdc-source"></a>Configurando a origem CDC  
 Você pode configurar a origem CDC programaticamente ou por meio do SSIS Designer.  
  
 Para obter mais informações, consulte um dos tópicos a seguir.  
  
-   [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [Editor de origem CDC &#40; Página colunas &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse na origem CDC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** , consulte [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [Editor de origem CDC &#40; Página colunas &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
-   [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Extrair dados de alteração por meio da origem CDC](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Modos de processamento para a origem de CDC](http://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/), em mattmasson.com.  
  
  
