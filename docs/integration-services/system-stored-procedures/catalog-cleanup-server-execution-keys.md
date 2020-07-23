---
title: catalog.cleanup_server_execution_keys | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a05de5d22c05c151d080ccf523b8577ba5b1033c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915633"
---
# <a name="catalogcleanup_server_execution_keys"></a>catalog.cleanup_server_execution_keys 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove certificados e chaves simétricas do banco de dados SSISDB.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cleanup_flag = ] *cleanup_flag*  
 Indica se os certificados e chaves simétricas no nível de execução (1) ou no nível do projeto (2) devem ser descartados.  
  
 Use o nível de execução (1) somente quando o SERVER_OPERATION_ENCRYPTION_LEVEL está definido como PER_EXECUTION (1).  
  
 Use o nível de projeto (2) somente quando o SERVER_OPERATION_ENCRYPTION_LEVEL está definido como PER_PROJECT (2). Certificados e chaves simétricas são removidas apenas para projetos que foram excluídos e para os quais os logs de operação foram limpos.  
  
 [ @delete_batch_size = ] *delete_batch_size*  
 O número de chaves e certificados a serem removidos. O valor padrão é 1000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 para êxito e 1 para falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e EXECUTE no projeto e, se aplicável, permissões READ no ambiente referenciado.  
  
-   Associação na função de banco de dados **ssis_admin**.  
  
-   Associação à função de servidor **sysadmin**.  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 Esse procedimento armazenado gera erros nos seguintes cenários:  
  
-   Há uma ou mais operações ativas no banco de dados SSISDB.  
  
-   O banco de dados SSISDB não está no modo de usuário único.  
  
## <a name="remarks"></a>Comentários  
 SQL Server 2012 Service Pack 2 adicionou a propriedade SERVER_OPERATION_ENCRYPTION_LEVEL à tabela **internal.catalog_properties**. Essa propriedade tem dois valores possíveis:  
  
-   **PER_EXECUTION (1)** – O certificado e a chave simétrica usados para proteger parâmetros de execução e logs de execução confidenciais são criados para cada execução. Esse é o valor padrão. Talvez você tenha problemas de desempenho (deadlocks, trabalhos de manutenção com falha, etc.) em um ambiente de produção porque chaves/certificado são gerados para cada execução. No entanto, essa configuração fornece um nível maior de segurança que o outro valor (2).  
  
-   **PER_PROJECT (2)** – O certificado e a chave simétrica usados para proteger parâmetros confidenciais são criados para cada projeto. Isso oferece um desempenho melhor do que o nível PER_EXECUTION porque a chave e o certificado são gerados uma vez para um projeto em vez de serem gerados para cada execução.  
  
 Você precisa executar o procedimento armazenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) antes de alterar o SERVER_OPERATION_ENCRYPTION_LEVEL de 1 para 2 ou de 2 para 1. Você precisa fazer o seguinte antes de executar este procedimento armazenado:  
  
1.  Verifique se o valor da propriedade OPERATION_CLEANUP_ENABLED está definido como TRUE na tabela [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
2.  Defina o SSISDB (banco de dados do Integration Services) para o modo de usuário único. No SQL Server Management Studio, inicie a caixa de diálogo Propriedades do Banco de Dados do SSISDB, mude para a guia Opções e defina a propriedade Restringir Acesso para o modo de usuário único (SINGLE_USER). Depois de executar o procedimento armazenado cleanup_server_log, defina o valor da propriedade para o valor original.  
  
3.  Execute o procedimento armazenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md).  
  
4.  Agora, vá em frente e altere o valor da propriedade SERVER_OPERATION_ENCRYPTION_LEVEL na tabela [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
5.  Execute o procedimento armazenado [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) para limpar as chaves de certificado do banco de dados SSISDB. Descartar certificados e chaves de banco de dados SSISDB pode levar muito tempo, então isso deve ser executado periodicamente fora dos horários de pico.  
  
     Você pode especificar o escopo ou o nível (execução versus projeto) e o número de chaves a serem excluídas. O tamanho de lote padrão para exclusão é 1000. Quando você define o nível para 2, as chaves e certificados serão excluídos somente se os projetos associados foram excluídos.  
  
 Para obter mais informações, veja o artigo da Base de Dados de Conhecimento a seguir. [CORREÇÃO: Problemas de desempenho ao usar o SSISDB como o repositório de implantação no SQL Server 2012](https://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama o procedimento armazenado cleanup_server_execution_keys.  
  
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
  
  
