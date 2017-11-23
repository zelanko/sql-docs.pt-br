---
title: Catalog.add_data_tap_by_guid | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9bd4ecb4a6a419f1965a349d46d16d764dd83708
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Adiciona um toque de dados a um caminho de fluxo de dados específico em um fluxo de dados de pacote, para uma instância da execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog add_data_tap_by_guid [ @execution_id = ] execution_id  
, [ @dataflow_task_guid = ] dataflow_task_guid   
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 A ID da execução que contém o pacote. O *execution_id* é um **bigint**.  
  
 [ @dataflow_task_guid =] *dataflow_task_guid*  
 O ID do fluxo de dados da tarefa no pacote que contém o caminho de fluxo de dados a ser tocado. O *dataflow_task_guid* é um**uniqueidentifier**.  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 A cadeia de caracteres de identificação para o caminho de fluxo de dados. Um caminho conecta dois componentes de fluxos de dados. O **IdentificationString** propriedade para o caminho Especifica a cadeia de caracteres.  
  
 Para localizar a cadeia de caracteres de identificação, em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] com o botão direito do caminho entre componentes de fluxo de dados e, em seguida, clique **propriedades**. O **IdentificationString** propriedade aparece no **propriedades** janela.  
  
 O *dataflow_path_id_string* é um **nvarchar (4000)**.  
  
 [ @data_filename =] *data_filename*  
 O nome do arquivo de dados que armazena os dados tocados. Se a tarefa de fluxo de dados for executada dentro de um contêiner de Loop Foreach ou Loop For, arquivos separados armazenarão os dados tocados para cada iteração do loop. Cada arquivo é prefixado com um número que corresponde a uma iteração. Arquivos de toque de dados são gravados na pasta "*\<pasta de instalação do SQL Server >*\130\DTS\\". O *data_filename* é um **nvarchar (4000)**.  
  
 [ @max_rows =] max_rows  
 O número de linhas capturadas durante o toque de dados. Se esse valor não for especificado, todas as linhas serão capturadas. O max_rows é um **int**.  
  
 [ @data_tap_id =] *data_tap_id*  
 A ID do toque de dados. O *data_tap_id* é um **bigint**.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, um toque de dados é criado no caminho de fluxo de dados, `Paths[SRC DimDCVentor.OLE DB Source Output]`, na tarefa de fluxo de dados `{D978A2E4-E05D-4374-9B05-50178A8817E8}`. Os dados tocados são armazenados no arquivo DCVendorOutput.csv.  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>Comentários  
 Para adicionar toques de dados, a instância da execução deve estar no estado criado (um valor de 1 no **status** coluna o [Catalog. Operations &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)exibição). O valor de estado muda quando você realiza a execução. Você pode criar uma execução chamando [Catalog. create_execution &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 As seguintes são considerações a respeito do procedimento armazenado add_data_tap_by_guid.  
  
-   Quando você adiciona um toque de dados, ele não é validado antes de o pacote ser executado.  
  
-   É recomendável limitar o número de linhas capturadas durante o toque de dados, para evitar gerar arquivos de dados grandes. Se a máquina na qual o procedimento armazenado é executado ficar sem espaço de armazenamento para os arquivos de dados, a execução do procedimento armazenado será interrompida.  
  
-   A execução do procedimento armazenado add_data_tap_by_guid afeta o desempenho do pacote. É recomendável executar o procedimento armazenado apenas para solucionar problemas de dados.  
  
-   Para acessar o arquivo que armazena os dados tocados, você deve ter permissões de administrador na máquina na qual o procedimento armazenado é executado ou deve ser o usuário que iniciou a execução que contém o pacote com toque de dados.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões MODIFY na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem permissões MODIFY.  
  
-   O toque de dados para o componente especificado, no pacote especificado, já foi adicionado.  
  
-   O valor especificado para o número de linhas a serem capturadas não é válido.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte também  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  

