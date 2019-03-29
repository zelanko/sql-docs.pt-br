---
title: catalog.add_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1f9edd63a9855bf87b653c0b4cbbdfffc5b70db
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280760"
---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Adiciona um toque de dados à saída de um componente em um fluxo de dados de pacote, para uma instância da execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.add_data_tap [ @execution_id = ] execution_id  
, [ @task_package_path = ] task_package_path  
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 A ID da execução que contém o pacote. O *execution_id* é um **bigint**.  
  
 [ @task_package_path = ] *task_package_path*  
 O caminho do pacote da tarefa de fluxo de dados. A propriedade **PackagePath** da tarefa de fluxo de dados especifica o caminho. O caminho diferencia maiúsculas de minúsculas. Para localizar o caminho do pacote, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique com o botão direito do mouse na tarefa Fluxo de Dados e, depois, clique em **Propriedades**. A propriedade **PackagePath** aparece na janela **Propriedades**.  
  
 O *task_package_path* é um **nvarchar(max)**.  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 A cadeia de caracteres de identificação para o caminho de fluxo de dados. Um caminho conecta dois componentes de fluxos de dados. A propriedade **IdentificationString** do caminho especifica a cadeia de caracteres.  
  
 Para localizar a cadeia de caracteres de identificação, no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique com o botão direito do mouse no caminho entre dois componentes de fluxo de dados e, depois, clique em **Propriedades**. A propriedade **IdentificationString** aparece na janela **Propriedades**.  
  
 O *dataflow_path_id_string* é um **nvarchar(4000)**.  
  
 [ @data_filename = ] *data_filename*  
 O nome do arquivo de dados que armazena os dados tocados. Se a tarefa de fluxo de dados for executada dentro de um contêiner de Loop Foreach ou Loop For, arquivos separados armazenarão os dados tocados para cada iteração do loop. Cada arquivo é prefixado com um número que corresponde a uma iteração.  
  
 Por padrão, o arquivo é armazenado na pasta \<*unidade*>:\Arquivos de Programas\Microsoft SQL Server\130\DTS\DataDumps.  
  
 O *data_filename* é um **nvarchar(4000)**.  
  
 [ @max_rows = ] *max_rows*  
 O número de linhas capturadas durante o toque de dados. Se esse valor não for especificado, todas as linhas serão capturadas. O *max_rows* é um **int**.  
  
 [ @data_tap_id = ] *data_tap_id*  
 Retorna a ID do toque de dados. O *data_tap_id* é um **bigint**.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, um toque de dados é criado no caminho do fluxo de dados, `'Paths[OLE DB Source.OLE DB Source Output]`, na tarefa de fluxo de dados, `\Package\Data Flow Task`. Os dados coletados são armazenados no arquivo `output0.txt` na pasta DataDumps (\<*unidade*>:\Arquivos de Programas\Microsoft SQL Server\130\DTS\DataDumps).  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Remarks  
 Para adicionar coletas de dados, a instância da execução deve estar no estado criado (um valor de 1 na coluna **status** da exibição [catalog.operations &#40;banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)). O valor de estado muda quando você realiza a execução. Você pode criar uma execução chamando [catalog.create_execution &#40;banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 As seguintes são considerações a respeito do procedimento armazenado add_data_tap.  
  
-   Se uma execução contiver um pacote pai e um ou mais pacotes filho, você precisará adicionar um toque de dados para cada pacote para o qual você deseja tocar dados.  
  
-   Se um pacote contiver mais de uma tarefa de fluxo de dados com o mesmo nome, o task_package_path identificará exclusivamente a tarefa de fluxo de dados que contém a saída do componente tocado.  
  
-   Quando você adiciona uma coleta de dados, ele não é validado antes de o pacote ser executado.  
  
-   É recomendável limitar o número de linhas capturadas durante o toque de dados, para evitar gerar arquivos de dados grandes. Se a máquina na qual o procedimento armazenado é executado ficar sem espaço de armazenamento para os arquivos de dados, a execução do pacote será interrompida e uma mensagem de erro será gravada em um log.  
  
-   A execução do procedimento armazenado add_data_tap impacta o desempenho do pacote. É recomendável executar o procedimento armazenado apenas para solucionar problemas de dados.  
  
-   Para acessar o arquivo que armazena os dados tocados, você deve ser um administrador na máquina na qual o procedimento armazenado é executado. Você também deve ser o usuário que iniciou a execução que contém o pacote com o toque de dados.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões MODIFY na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem permissões MODIFY.  
  
-   O toque de dados para o componente especificado, no pacote especificado, já foi adicionado.  
  
-   O valor especificado para o número de linhas a serem capturadas não é válido.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [SSIS 2012: um olhar sobre fontes de dados](https://go.microsoft.com/fwlink/?LinkId=239983), em rafael-salas.com.  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
