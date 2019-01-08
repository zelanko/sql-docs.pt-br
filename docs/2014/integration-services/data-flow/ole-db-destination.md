---
title: Destino OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdest.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0aedda782c65cbe8d28f066b7e5e97d3e7fc87cd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790768"
---
# <a name="ole-db-destination"></a>Destino OLE DB
  O destino OLE DB carrega os dados em uma variedade de bancos de dados compatíveis com OLE DB usando uma tabela ou exibição de banco de dados ou um comando SQL. Por exemplo, a fonte OLE DB pode carregar dados em tabelas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access e nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O destino OLE DB fornece cinco modos diferentes de acesso para carregar dados:  
  
-   Uma tabela ou exibição. Você pode especificar uma tabela ou exibição existente ou criar uma tabela nova.  
  
-   Uma tabela ou exibição que usa opções de carregamento rápido. Você pode especificar uma tabela existente ou criar uma tabela nova.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Uma tabela ou exibição especificada em uma variável que usa opções de carregamento rápido.  
  
-   Os resultados de uma instrução SQL.  
  
> [!NOTE]  
>  O destino OLE DB não aceita parâmetros. Se você precisar executar uma instrução parametrizada INSERT, considere a transformação Comando OLE DB. Para obter mais informações, consulte [OLE DB Command Transformation](transformations/ole-db-command-transformation.md).  
  
 Quando o destino OLE DB carrega dados que usam o conjunto de caracteres de dois bytes (DBCS), os dados poderão ser corrompidos se o modo de acesso de dados não usar a opção de carregamento rápido e se o gerenciador de conexões OLE DB usar o provedor OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Para garantir a integridade dos dados DBCS, você deve configurar o Gerenciador de conexão OLE DB para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ou utilizar um dos modos de acesso de carregamento rápido: **Tabela ou exibição – carregamento rápido** ou **tabela ou exibição variável de nome - carregamento rápido**. As duas opções estão disponíveis na caixa de diálogo **Editor de Destino de OLE DB** . Ao programar o [!INCLUDE[ssIS](../../includes/ssis-md.md)] modelo de objeto, você deve definir a propriedade AccessMode `OpenRowset Using FastLoad`, ou `OpenRowset Using FastLoad From Variable`.  
  
> [!NOTE]  
>  Se você usar a caixa de diálogo **Editor de Destino de OLE DB** no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer para criar a tabela de destino em que o destino OLE DB insere dados, você poderá ter que selecionar a nova tabela manualmente. A necessidade de selecionar manualmente ocorre quando um provedor OLE DB, como o provedor OLE DB para DB2, adiciona automaticamente identificadores de esquema ao nome da tabela.  
  
> [!NOTE]  
>  A instrução CREATE TABLE gerada pela caixa de diálogo **Editor de Destino de OLE DB** pode requerer modificação dependendo do tipo de destino. Por exemplo, alguns destinos não suportam os tipos de dados que a instrução CREATE TABLE usa.  
  
 Esse destino usa um gerenciador de conexões OLE DB para conectar-se a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual você pode criar um gerenciador de conexões OLE DB, disponibilizando as fontes de dados e exibições da fonte de dados para o destino OLE DB.  
  
 Um destino OLE DB inclui mapeamentos entre as colunas de entrada e as colunas da fonte de dados de destino. Você não precisa mapear as colunas de entrada para todas as colunas de destino, mas, dependendo das propriedades das colunas de destino, podem ocorrer erros se nenhuma das colunas de entrada for mapeada para as colunas de destino. Por exemplo, se uma coluna de destino não permitir valores nulos, uma coluna de entrada deve ser mapeada para aquela coluna de destino. Além disso, os tipos de dados de colunas mapeadas devem ser compatíveis. Por exemplo, você não pode mapear uma coluna de entrada que tenha um tipo de dados de cadeia de caracteres para uma coluna com um tipo de dados numérico.  
  
 O destino OLE DB tem uma entrada regular e uma saída de erro.  
  
 Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Opções de carregamento rápido  
 Se o destino OLE DB usa um modo de acesso a dados de carregamento rápido, você pode especificar as seguintes opções na interface do usuário, **Editor de Destino de OLE DB**, para esse destino:  
  
-   Manter os valores de identidade do arquivo de dados importado ou usar valores exclusivos atribuídos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Reter um valor nulo durante a operação de carregamento em massa.  
  
-   Verificar restrições na tabela ou exibição de destino durante a operação de importação em massa.  
  
-   Adquirir um bloqueio em nível de tabela pela duração da operação de carregamento em massa.  
  
-   Especificar o número de linhas no lote e o tamanho de confirmação.  
  
 Algumas opções de carregamento rápido são armazenadas em propriedades específicas do destino OLE DB. Por exemplo, FastLoadKeepIdentity especifica se os valores de identidade são mantidos ou não, FastLoadKeepNulls especifica se valores nulos são mantidos ou não e FastLoadMaxInsertCommitSize especifica o número de linhas a serem confirmadas como um lote. Outras opções de carregamento rápido são armazenadas em uma lista separada por vírgulas na propriedade FastLoadOptions. Se o destino de OLE DB usa todas as opções de carregamento rápido que são armazenadas em FastLoadOptions e listadas na **Editor de destino do OLE DB** caixa de diálogo, o valor da propriedade é definido como `TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000`. O valor 1000 indica que o destino é configurado para usar lotes de 1000 linhas.  
  
> [!NOTE]  
>  Qualquer falha de restrição ao destino fará com que todo o lote de linhas definido por FastLoadMaxInsertCommitSize falhe.  
  
 Além das opções de carregamento rápido apresentadas na caixa de diálogo **Editor de Destino de OLE DB** , você pode configurar o destino OLE DB para usar as seguintes opções de carregamento em massa informando-as na propriedade FastLoadOptions na caixa de diálogo **Editor Avançado** .  
  
|Opção de carregamento rápido|Descrição|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Especifica o tamanho em quilobytes a ser inserido. A opção tem o formato `KILOBYTES_PER_BATCH`  =  \<valor inteiro positivo**>**.|  
|FIRE_TRIGGERS|Especifica se os gatilhos devem ser disparados na tabela de inserção. A opção tem o formato **FIRE_TRIGGERS**. A presença da opção indica que os gatilhos irão disparar.|  
|ORDER|Especifica como os dados de entrada são classificados. A opção tem o formato ORDER \<nome da coluna> ASC&#124;DESC. Qualquer número de colunas pode ser listado e a inclusão da ordem de classificação é opcional. Se a ordem de classificação for omitida, a operação de inserção assumirá que os dados não estão classificados.<br /><br /> Observação: O desempenho pode ser otimizado se você usar a opção ORDER para classificar os dados de entrada de acordo com o índice clusterizado da tabela.|  
  
 As palavras-chave [!INCLUDE[tsql](../../includes/tsql-md.md)] são normalmente digitadas em letras maiúsculas, mas não fazem distinção entre maiúsculas e minúsculas.  
  
 Para saber mais sobre opções de carregamento rápido, consulte [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Solucionando problemas do destino OLE DB  
 Você pode registrar as chamadas que o destino OLE DB faz para provedores de dados externos. Você pode usar esse recurso de registro para solucionar problemas ao salvar os dados em fontes de dados externas que o destino OLE DB executa. Para registrar as chamadas que o destino OLE DB faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Configurando o destino OLE DB  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destino de OLE DB** clique em um dos seguintes tópicos:  
  
-   [Editor de Destino OLE DB &#40;Página Gerenciador de Conexões&#41;](../ole-db-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destino de OLE DB &#40;Página Mapeamentos&#41;](../ole-db-destination-editor-mappings-page.md)  
  
-   [Editor de Destino OLE DB &#40;Página Saída de Erro&#41;](../ole-db-destination-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas OLE DB](ole-db-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Carregar dados por meio do destino OLE DB](ole-db-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Origem de OLE DB](ole-db-source.md)  
  
 [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services-ssis-variables.md)  
  
 [Fluxo de Dados](data-flow.md)  
  
  
