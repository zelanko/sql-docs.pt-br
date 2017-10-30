---
title: add_data_tap | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 686b40e7e1ad7f7843bee5af3295fdf394538f63
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [ @execution_id =] *execution_id*  
 A ID da execução que contém o pacote. O *execution_id* é um **bigint**.  
  
 [ @task_package_path =] *task_package_path*  
 O caminho do pacote da tarefa de fluxo de dados. O **PackagePath** propriedade para a tarefa de fluxo de dados especifica o caminho. O caminho diferencia maiúsculas de minúsculas. Para localizar o caminho de pacote, em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] clique a tarefa de fluxo de dados e, em seguida, clique em **propriedades**. O **PackagePath** propriedade aparece no **propriedades** janela.  
  
 O *task_package_path* é um **nvarchar (max)**.  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 A cadeia de caracteres de identificação para o caminho de fluxo de dados. Um caminho conecta dois componentes de fluxos de dados. O **IdentificationString** propriedade para o caminho Especifica a cadeia de caracteres.  
  
 Para localizar a cadeia de caracteres de identificação, em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] com o botão direito do caminho entre componentes de fluxo de dados e, em seguida, clique **propriedades**. O **IdentificationString** propriedade aparece no **propriedades** janela.  
  
 O *dataflow_path_id_string* é um **nvarchar (4000)**.  
  
 [ @data_filename =] *data_filename*  
 O nome do arquivo de dados que armazena os dados tocados. Se a tarefa de fluxo de dados for executada dentro de um contêiner de Loop Foreach ou Loop For, arquivos separados armazenarão os dados tocados para cada iteração do loop. Cada arquivo é prefixado com um número que corresponde a uma iteração.  
  
 Por padrão, o arquivo é armazenado no \< *unidade*>: pasta \Program Files\Microsoft Server\130\DTS\DataDumps SQL.  
  
 O *data_filename* é um **nvarchar (4000)**.  
  
 [ @max_rows =] *max_rows*  
 O número de linhas capturadas durante o toque de dados. Se esse valor não for especificado, todas as linhas serão capturadas. O *max_rows* é um **int**.  
  
 [ @data_tap_id =] *data_tap_id*  
 Retorna a ID do toque de dados. O *data_tap_id* é um **bigint**.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, um toque de dados é criado no caminho do fluxo de dados, `'Paths[OLE DB Source.OLE DB Source Output]`, na tarefa de fluxo de dados, `\Package\Data Flow Task`. Os dados tocados são armazenados no `output0.txt` arquivo na pasta DataDumps (\<*unidade*>: \Program Files\Microsoft Server\130\DTS\DataDumps SQL).  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Comentários  
 Para adicionar toques de dados, a instância da execução deve estar no estado criado (um valor de 1 no **status** coluna o [Catalog. Operations &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)exibição). O valor de estado muda quando você realiza a execução. Você pode criar uma execução chamando [Catalog. create_execution &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 As seguintes são considerações a respeito do procedimento armazenado add_data_tap.  
  
-   Se uma execução contiver um pacote pai e um ou mais pacotes filho, você precisará adicionar um toque de dados para cada pacote para o qual você deseja tocar dados.  
  
-   Se um pacote contiver mais de uma tarefa de fluxo de dados com o mesmo nome, o task_package_path identificará exclusivamente a tarefa de fluxo de dados que contém a saída do componente tocado.  
  
-   Quando você adiciona um toque de dados, ele não é validado antes do pacote é executado.  
  
-   É recomendável limitar o número de linhas capturadas durante o toque de dados, para evitar gerar arquivos de dados grandes. Se a máquina na qual o procedimento armazenado é executado ficar sem espaço de armazenamento para os arquivos de dados, a execução do pacote será interrompida e uma mensagem de erro será gravada em um log.  
  
-   A execução do procedimento armazenado add_data_tap impacta o desempenho do pacote. É recomendável executar o procedimento armazenado apenas para solucionar problemas de dados.  
  
-   Para acessar o arquivo que armazena os dados tocados, você deve ser um administrador na máquina na qual o procedimento armazenado é executado. Você também deve ser o usuário que iniciou a execução que contém o pacote com o toque de dados.  
  
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
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [SSIS 2012: A exibição de dados](http://go.microsoft.com/fwlink/?LinkId=239983), em rafael-salas.com.  
  
## <a name="see-also"></a>Consulte também  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  

