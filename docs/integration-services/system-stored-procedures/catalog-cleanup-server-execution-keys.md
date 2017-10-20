---
title: Catalog.cleanup_server_execution_keys | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 172925d5a63aa831881b6a6325f0dbcbccd4dd56
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverexecutionkeys"></a>Catalog.cleanup_server_execution_keys
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Remove certificados e chaves simétricas do banco de dados SSISDB.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cleanup_flag =] *cleanup_flag*  
 Indica se o nível de execução (1) ou o projeto de nível (2) certificados e chaves simétricas devem ser descartados.  
  
 Use o nível de execução (1) somente quando o SERVER_OPERATION_ENCRYPTION_LEVEL é definido como PER_EXECUTION (1).  
  
 Use o nível de projeto (2) somente quando o SERVER_OPERATION_ENCRYPTION_LEVEL é definido como PER_PROJECT (2). Certificados e chaves simétricas são removidas apenas para projetos que foram excluídos e para o qual os logs de operação foram limpos.  
  
 [ @delete_batch_size =] *delete_batch_size*  
 O número de chaves e certificados a serem removidos. O valor padrão é 1000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 para êxito e 1 para falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e EXECUTE no projeto e, se aplicável, permissões de leitura no ambiente referenciado.  
  
-   Associação de **ssis_admin** função de banco de dados.  
  
-   Associação de **sysadmin** função de servidor.  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 Esse procedimento armazenado gera erros nos seguintes cenários:  
  
-   Há uma ou mais operações ativas no banco de dados SSISDB.  
  
-   O banco de dados SSISDB não está no modo de usuário único.  
  
## <a name="remarks"></a>Comentários  
 SQL Server 2012 Service Pack 2 adicionada a propriedade SERVER_OPERATION_ENCRYPTION_LEVEL para o **internal.catalog_properties** tabela. Essa propriedade tem dois valores possíveis:  
  
-   **PER_EXECUTION (1)** – o certificado e a chave simétrica usada para proteger os parâmetros de execução confidenciais e logs de execução são criados para cada execução. Este é o valor padrão. Você pode executar em problemas de desempenho (deadlocks, manutenção com falha trabalhos etc...) em um ambiente de produção porque/chaves de certificado são geradas para cada execução. No entanto, essa configuração fornece um nível maior de segurança que o outro valor (2).  
  
-   **PER_PROJECT (2)** – o certificado e a chave simétrica usada para proteger os parâmetros confidenciais são criados para cada projeto. Isso fornece um desempenho melhor do que o nível PER_EXECUTION porque a chave e o certificado são gerados uma vez para um projeto em vez de cada execução.  
  
 Você precisa executar o [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) procedimento armazenado antes de alterar o SERVER_OPERATION_ENCRYPTION_LEVEL entre 1 e 2 (ou) de 2 para 1. Antes de executar esse procedimento armazenado, faça o seguinte:  
  
1.  Verifique se o valor da propriedade OPERATION_CLEANUP_ENABLED está definido como TRUE no [Catalog. catalog_properties &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) tabela.  
  
2.  Defina o banco de dados do Integration Services (SSISDB) para o modo de usuário único. No SQL Server Management Studio, iniciar a caixa de diálogo Propriedades do banco de dados do SSISDB, alterne para a guia Opções e defina a propriedade de restringir o acesso para o modo de usuário único (SINGLE_USER). Depois de executar o cleanup_server_log procedimento armazenado, defina o valor da propriedade para o valor original.  
  
3.  Execute o procedimento armazenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md).  
  
4.  Agora, vá em frente e altere o valor da propriedade SERVER_OPERATION_ENCRYPTION_LEVEL no [Catalog. catalog_properties &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) tabela.  
  
5.  Execute o procedimento armazenado [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) para limpar as chaves de certificados do banco de dados SSISDB. Descartando certificados e chaves de banco de dados SSISDB pode levar muito tempo, para que ele deve ser executado periodicamente durante horários de pico.  
  
     Você pode especificar o escopo ou o nível (execução versus projeto) e o número de chaves a ser excluído. O tamanho de lote padrão para exclusão é 1000. Quando você definir o nível 2, as chaves e certificados são excluídos somente se os projetos associados foram excluídos.  
  
 Para obter mais informações, consulte o seguinte artigo da Base de dados de Conhecimento. [CORREÇÃO: Problemas de desempenho ao usar o SSISDB como sua implantação armazenam no SQL Server 2012](http://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama o procedimento armazenado de cleanup_server_execution_keys.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
  
EXEC@return_value = [internal].[cleanup_server_execution_keys]  
@cleanup_flag = 1,  
@delete_batch_size = 500  
  
SELECT'Return Value' = @return_value  
  
GO  
```  
  
  
